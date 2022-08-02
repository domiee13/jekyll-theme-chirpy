---
title: Are you the admin? TFCCTF 2022
date: 2022-08-02 07:00:00 +0700
categories: [Writeup, TFCCTF 2022]
tags: [web, writeup]     # TAG names should always be lowercase
---

# ARE YOU THE ADMIN? - TFCCTF2022

![Untitled](/assets/img/AREYOUTHEADMIN/Untitled.png)

Source code đi kèm

**schema.prisma**

```jsx
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "sqlite"
  url      = "file:./app.db"
}

model User {
  id       String  @id @default(uuid())
  username String
  isAdmin  Boolean @default(false)
}
```

**auth.ts**

```jsx
import { NextApiRequest, NextApiResponse } from "next";
import { prisma } from "../../globals/prisma";

export default async function handler(
  req: NextApiRequest,
  res: NextApiResponse
) {
  const body = req.body;
  await prisma.user.create({
    data: body,
  });
  return res.status(200).end();
}
```

**index.tsx**

```jsx
import type { GetServerSideProps, NextPage } from "next";
import type { User } from "@prisma/client";
import { prisma } from "../globals/prisma";
import { useState } from "react";
import { useRouter } from "next/router";

type Props = {
  users: (User &
    (
      | {
          flag: string;
          isAdmin: true;
        }
      | {
          flag?: never;
          isAdmin: false;
        }
    ))[];
};

const Home: NextPage<Props> = ({ users }) => {
  const [username, setUsername] = useState("");

  const router = useRouter();

  const create = async () => {
    await fetch("/api/auth", {
      headers: {
        "Content-Type": "application/json",
      },
      method: "POST",
      body: JSON.stringify({
        username,
      }),
    });
    await router.replace(router.asPath);
  };

  return (
    <div>
      <div>Create user:</div>
      <input
        value={username}
        onChange={(event) => setUsername(event.target.value)}
      />
      <button onClick={create}>Create</button>
      <div>Users:</div>
      {users.map((user) => (
        <div key={user.id}>
          <div>Username: {user.username}</div>
          <div>Is admin? {user.isAdmin ? "yes" : "no"}</div>
          {user.isAdmin && <div>{user.flag}</div>}
        </div>
      ))}
    </div>
  );
};

export default Home;

export const getServerSideProps: GetServerSideProps<Props> = async (
  context
) => {
  const users = (await prisma.user.findMany()) as Props["users"];

  for (const user of users) {
    if (user.isAdmin) {
      user.flag = process.env.FLAG!;
    }
  }

  return {
    props: {
      users,
    },
  };
};
```

Trang web rất đơn giản, gồm 1 cái form để điền username và nút Create

![Untitled](/assets/img/AREYOUTHEADMIN/Untitled%201.png)

![Untitled](/assets/img/AREYOUTHEADMIN/Untitled%202.png)

Khi click vào button Create, web sẽ POST đến endpoint /api/auth với body là username

![Untitled](/assets/img/AREYOUTHEADMIN/Untitled%203.png)

Đọc code để xem endpoint /api/auth sẽ làm gì

Theo mình hiểu thì nó sẽ lấy dữ liệu được POST lên và tạo 1 user mới

![Untitled](/assets/img/AREYOUTHEADMIN/Untitled%204.png)

Nếu user là admin, web sẽ lấy flag và in ra 

![Untitled](/assets/img/AREYOUTHEADMIN/Untitled%205.png)

Ok quay trở lại với request create user

![Untitled](/assets/img/AREYOUTHEADMIN/Untitled%206.png)

Vì /api/auth không hề check lại body hay lọc dữ liệu mà chỉ lấy toàn bộ body nên mình chỉ cần thêm trường “isAdmin”:true

![Untitled](/assets/img/AREYOUTHEADMIN/Untitled%207.png)

Ok ngon lành

![Untitled](/assets/img/AREYOUTHEADMIN/Untitled%208.png)

![Untitled](/assets/img/AREYOUTHEADMIN/Untitled%209.png)

```jsx
Flag: TFCCTF{S4n1t1z3_Y0ur_1nput5!}
```