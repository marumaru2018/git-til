## Error Type

Build Error

## Error Message

Module not found: Can't resolve 'jose'

## Build Output

./app/utils/useAuth.tsx:3:1
Module not found: Can't resolve 'jose'
1 | import { useRouter } from "next/navigation";
2 | import { useEffect, useState } from "react";

> 3 | import { jwtVerify } from "jose";

    | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

4 |
5 | const useAuth = () => {
6 | const [loginUserEmail, setLoginUserEmail] = useState<string>("");

Import traces:
Client Component Browser:
./app/utils/useAuth.tsx [Client Component Browser]
./app/item/create/page.tsx [Client Component Browser]
./app/item/create/page.tsx [Server Component]

Client Component SSR:
./app/utils/useAuth.tsx [Client Component SSR]
./app/item/create/page.tsx [Client Component SSR]
./app/item/create/page.tsx [Server Component]

https://nextjs.org/docs/messages/module-not-found

Next.js version: 16.0.3 (Turbopack)

## 原因と対応
