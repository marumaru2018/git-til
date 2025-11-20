## Error Type

Runtime Error

## Error Message

Invalid src prop (https://res.cloudinary.com/dqtzs1hhi/image/upload/v1763679375/qlx78xys93g93fd3nuhz.jpg) on `next/image`, hostname "res.cloudinary.com" is not configured under images in your `next.config.js`
See more info: https://nextjs.org/docs/messages/next-image-unconfigured-host

    at <anonymous> (app\page.tsx:55:15)
    at Array.map (<anonymous>:1:18)
    at ReadAllItems (app\page.tsx:39:17)

## Code Frame

53 | return (
54 | <Link href={`/item/read/${item.id}`} key={item.id}>

> 55 | <Image

     |               ^

56 | src={imageSrc}
57 | width={750}
58 | height={500}

Next.js version: 16.0.3 (Turbopack)
