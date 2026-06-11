# Code in XML

Add syntax highlighting to embedded code blocks inside XML files. Supported languages are:  

- `<groovy>`
- `<java>`
- `<javascript>`
- `<python>`
- `<ruby>`
- `<sql>` | MyBatis tags (`<select>` / `<insert>` / `<update>` / `<delete>`)
- `<bash>` | `<shell>` | `<sh>`

---

🌸 **Japanese note**  
XMLファイルに記述した上記言語に対し各言語のハイライトをします。ハイライトは対象言語の拡張を追加してください。  

---

I initially created this extension to help my team work with XML DSL files containing embedded Groovy code snippets for Apache Camel. Since it proved useful, I expanded it to support other languages like JS, SQL, and MyBatis mapper tags like `<select>`, `<insert>`, and so on.  
Here are sample XML DSL file images before and after applying this extension's syntax highlighting:  

![XML Sample Before Image](images/xml-sample-before.png)

I hope this syntax highlighting helps you read code more easily and quickly:

![XML Sample After Image](images/xml-sample-after.png)

---

## ✨ Features

- ✅ Syntax highlighting for embedded code blocks inside XML
- ✅ Supports both CDATA and inline content
- ✅ The surrounding XML remains fully highlighted
- ✅ Native support for MyBatis mapper tags (`<select>`, `<insert>`, `<update>`, `<delete>`)
- ✅ Supports multiple SQL dialects (Oracle, MySQL, PostgreSQL)

## 📋 Required Extensions

For full syntax highlighting, install language extensions based on the languages you use (for example):

- **Java**: [Extension Pack for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack) (Microsoft)
- **Python**: [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) (Microsoft)
- **Groovy**: [Groovy Language Support](https://marketplace.visualstudio.com/items?itemName=marlon407.code-groovy) or similar
- **Ruby**: [Ruby](https://marketplace.visualstudio.com/items?itemName=shopify.ruby-lsp) (Shopify)
- **SQL**: [SQLTools](https://marketplace.visualstudio.com/items?itemName=mtxr.sqltools) (mtxr), [SQL Server](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) (Microsoft), or [PostgreSQL](https://marketplace.visualstudio.com/items?itemName=ms-ossdata.vscode-pgsql) (Microsoft)
- **JavaScript**: Built-in to VS Code

Optional XML support:

- [XML](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-xml)
- [XML Tools](https://marketplace.visualstudio.com/items?itemName=DotJoshJohnson.xml)

---

## 💡 Usage Examples

### Language Blocks

#### Java Block

```xml
<java>
  public class Greeter {
    public String greet(String name) {
      return "Hello, " + name + "!";
    }
  }
</java>
```

#### Python Block

```xml
<python>
  def greet(name):
      return f"Hello, {name}!"
  
  items = ['apple', 'banana', 'cherry']
  for item in items:
      print(item)
</python>
```

#### JavaScript with CDATA

```xml
<javascript><![CDATA[
  function sayHi(name) {
    return `Hi, ${name}!`;
  }
  console.log(sayHi("Smith"));
]]></javascript>
```

#### Groovy Block

```xml
<groovy>
  println "Hello from Groovy!"
  def items = ['apple', 'banana', 'cherry']
  items.each { println it }
</groovy>
```

#### Generic Language Attribute Format

```xml
<language language="sql">
  SELECT * FROM products WHERE status = 'active'
</language>
```

#### Shell Script Block

```xml
<bash><![CDATA[
#!/usr/bin/env bash
set -euo pipefail

echo "start job"
for file in /data/in/*.csv; do
  echo "processing: $file"
done
]]></bash>
```

### Whole XML

#### Apache Camel XML DSL

```xml
<route>
  <from uri="direct:start"/>
  <process>
    <script language="python">
      message.body = message.body.upper()
    </script>
  </process>
  <to uri="direct:end"/>
</route>
```

#### MyBatis Mapper XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Config 3.0//EN" 
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="com.example.repository.UserRepository">
  <select id="getUserById" parameterType="int">
    SELECT id, name, email 
    FROM users 
    WHERE id = #{id}
  </select>

  <insert id="insertUser" parameterType="com.example.model.User"><![CDATA[
    INSERT INTO users (name, email, created_date)
    VALUES (#{name}, #{email}, SYSDATE)
  ]]></insert>

  <update id="updateUserEmail" parameterType="map"><![CDATA[
    UPDATE users 
    SET email = #{email},
        modified_date = NOW()
    WHERE id = #{id}
  ]]></update>

  <delete id="deleteUser" parameterType="int">
    DELETE FROM users WHERE id = #{id}
  </delete>
</mapper>
```

---

## 📂 File Types

This extension targets `.xml` files.  

---

## 🚀 Installation

Install via [Code in XML](https://marketplace.visualstudio.com/items?itemName=okkeng.vscode-code-in-xml) on the Visual Studio Code Marketplace  
_or_  
Manually install from `.vsix`:  

```sh
code --install-extension vscode-code-in-xml-1.0.0.vsix
```

---

## 📝 Notes

- This extension provides syntax highlighting for embedded code by delegating language recognition to VS Code built-in grammars and installed language extensions
- SQL support is particularly useful for **MyBatis** XML mappers, which often contain complex SQL with comments and special syntax
- The extension works with both inline code and CDATA sections
- Supported SQL dialects include Oracle, MySQL, and PostgreSQL (through the installed SQL extension)
- VS Code built-in JavaScript grammar is used automatically (for `source.js` highlight)

If you use Apache Camel or Spring Integration with Java, add the necessary libraries to your project. See:  

- [Apache Camel > Expression Languages](https://camel.apache.org/components/latest/languages/index.html)
- [Spring Integration > Java DSL](https://docs.spring.io/spring-integration/reference/dsl.html)

---

## 📝 Known Issues

- In very nested XML structures, some themes may ignore embedded scopes
- In embedded code, words such as `name` and `status` in SQL may be highlighted as keywords by your installed language extension when they match reserved words.

---

## 📌 Release Notes

### v1.0.0 - June 11, 2026

- Added SQL highlighting support for XML-embedded SQL blocks.
- Added MyBatis mapper tag support: `<select>`, `<insert>`, `<update>`, and `<delete>`.
- Added SQL language attribute support: `<language language="sql">`.
- Added shell script tag support: `<bash>`, `<shell>`, and `<sh>`.
- Added shell language attribute support: `<language language="bash|shell|sh">`.
- Added test resources for Java, Python, MyBatis SQL, and shell script patterns.
- Updated README and extension metadata for official release.
- Changed the icon colors from gray/white to black/white/orange.

### v0.0.2

- Added support for `<python>` blocks inside XML.
- Changed the extension icon from auto-generated by Microsoft Copilot to one made by myself.
- Revised README by myself from auto-generated by Microsoft Copilot.

### v0.0.1

- Initial support for `<groovy>` and `<javascript>` blocks inside XML  
- CDATA and non-CDATA modes supported

---

## 🛠️ License

This project is licensed under the [MIT License](LICENSE).  
Copyright (c) 2025-2026 okkeng.  

---

## 🙌 Credits

This extension delegates embedded-language highlighting to VS Code and installed language extensions.
It does not bundle or redistribute third-party grammars.

- Visual Studio Code built-in language support
- User-installed language extensions (for Groovy, Python, Ruby, SQL, and others)
