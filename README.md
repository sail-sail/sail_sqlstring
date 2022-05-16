# sail_sqlstring

Simple SQL escape and format for MySQL for deno

## usage
```ts
import { assertEquals } from "https://deno.land/std@0.139.0/testing/asserts.ts";
import { escape, escapeId, format } from "https://deno.land/x/sail_sqlstring@v1.0.0/mod.ts";

Deno.test("escape", function() {
  const userId = "1";
  const sql = `select * from user where id = ${ escape(userId) }`;
  assertEquals(sql, "select * from user where id = '1'");
});

Deno.test("escapeId", function() {
  const user = "user";
  const sql = `select * from ${ escapeId(user) } where id = '1'`;
  assertEquals(sql, "select * from `user` where id = '1'");
});

Deno.test("format", function() {
  const sql = `select * from user where id = ?`;
  const sql2 = format(sql, [ "1" ]);
  assertEquals(sql2, "select * from user where id = '1'");
});
```
