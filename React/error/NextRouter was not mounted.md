## Error Type

Runtime Error

## Error Message

NextRouter was not mounted. https://nextjs.org/docs/messages/next-router-not-mounted

    at Login (app/user/login/page.tsx:9:27)

## Code Frame

```
   7 |   const [password, setPassword] = useState("");
   8 |
>  9 |   const router = useRouter();
     |                           ^
  10 |
  11 |   const handleSubmit = async (e: { preventDefault: () => void }) => {
  12 |     e.preventDefault();

Next.js version: 16.0.3 (Turbopack)
```

## 原因と対応

誤）import { useRouter } from "next/router";
正）import { useRouter } from "next/navigation";
