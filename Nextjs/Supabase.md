# Next.js から Spabase に接続する

インストール

```
npm i @supabase/supabase-js
```

# DB 接続

```api/utils/database.tsx
import { createClient } from "@supabase/supabase-js";

const supabase = createClient(
  "https://poiwfjhqdzgnqwrlqgcz.supabase.co",
);

export default supabase;
```

## データ読み込み

```
import { NextResponse } from "next/server"
import supabase from "../../../utils/database"

export const dynamic = "force-dynamic"

export async function GET(){
try{
const { data, error } = await supabase.from("items")
.select()
.order("created_at", {ascending: true})
if(error) throw new Error(error.message)
return NextResponse.json({message: "アイテム読み取り成功（オール）", allItems: data})
}catch(err){
return NextResponse.json({message: `アイテム読み取り失敗（オール）：${err}`})
}
}
```
