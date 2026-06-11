# Change Log

All notable changes to the "vscode-code-in-xml" extension will be documented in this file.

Check [Keep a Changelog](http://keepachangelog.com/) for recommendations on how to structure this file.

## [1.0.0] - 2026-06-11

### Added

- SQL support for MyBatis XML mappers and SQL-embedded XML formats
- MyBatis native tags: `<select>`, `<insert>`, `<update>`, `<delete>` with syntax highlighting
- Support for multiple SQL dialects: Oracle, MySQL, PostgreSQL
- SQL language attribute support: `<language language="sql">`
- Shell script tag support: `<bash>`, `<shell>`, and `<sh>`
- Shell language attribute support: `<language language="bash|shell|sh">`
- Test files for Java, Python, MyBatis SQL, and shell script patterns

### Changed

- Enhanced README with comprehensive examples for all supported languages
- Expanded keywords to include MyBatis
- Improved documentation for required language extensions
- Changed the icon colors from gray/white to black/white/orange

### Supported Languages

- Java, Groovy, Python, JavaScript, Ruby (since 0.0.1+)
- SQL (new in 1.0.0)
- Shell script (new in 1.0.0)

## [0.0.2] - 2025-07-03

- Added Python, Ruby support

## [0.0.1] - 2025-06-23

- Initial release with Groovy, Java, JavaScript support
