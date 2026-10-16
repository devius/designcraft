# Georgian interface

> **Last reviewed:** 2026-10-13 · **Last updated:** 2026-10-17 · **Change:** minor (catalog synced with upstream) · **Target:** DesignCraft 0.7.1

Choose **Edit › Interface Language › ქართული**. The catalog code is `ka`; the control and MCP command
`app.language` with `{"lang":"ka"}` selects it explicitly. The choice is saved with the other
interface settings (the macOS menu bar follows on the next launch). The desktop app does not follow the
system language (`ka`, `ka-GE`, `ka_GE.UTF-8`) yet; English is the default until a language is chosen.
The web build starts in `?lang=ka`, else in the first of the browser's languages that has a catalog
(`ka`, `ka-GE`). Document text, command ids, CLI/MCP/control responses and file paths do not
change.

`crates/ui-egui/src/i18n/ka.rs` has 2,370 entries: every key of the shared, Arabic, Brazilian
Portuguese, Czech, French, German, Italian, Japanese, Polish, Russian and Ukrainian tables, plus the
labels that only the code, the command table or the Tools panel use. It covers the menus, panels, dialogs, tools, built-in style and swatch names, and status
captions. Lower-layer engine and import messages keep their English wording, as in the other
languages. It is written from the meaning of the English labels; no proprietary translation
resources were consulted.

Georgian is also a text language for documents (character and paragraph language), separate from
the interface language.

## Georgian script

- **No case.** Mkhedruli has no upper and lower case. Change Case › Title Case and Sentence case
  leave Georgian letters alone, and index section heads stay Mkhedruli; UPPERCASE follows Unicode
  and gives Mtavruli (`ᲐᲑᲒ`). The interface never uses Mtavruli, and commands are verbal nouns
  (`შენახვა`, `განთავსება…`).
- **Counts** are count-neutral, noun first (`გვერდი: 5`): `count_label` writes `noun: n` for `ka`.
- **Fonts:** neither the bundle nor craft-fonts has a Georgian face yet. On desktop,
  `theme::add_system_fallbacks` appends an installed face for the Georgian script (Segoe UI, Sylfaen,
  Noto Sans Georgian or DejaVu Sans) and ships nothing. The web build fetches
  `fonts/NotoSansGeorgian.ttf` when the site serves one beside the page; without it Georgian draws as
  boxes until an OFL Georgian face is added to craft-fonts.

## Terminology

| Source | Georgian |
|---|---|
| File / Edit / View / Window | ფაილი / რედაქტირება / ჩვენება / ფანჯარა |
| Layout | განლაგება |
| Type (menu) | ტექსტი |
| Object / Table | ობიექტი / ცხრილი |
| Place… / Package… | განთავსება… / შეფუთვა… |
| Paste / Undo / Redo | ჩასმა / დაბრუნება / ხელახლა შესრულება |
| Pages / Spread | გვერდები / გაშლა |
| New Parent… | ახალი საბაზო გვერდი… |
| Layers / Swatches | შრეები / ფერის ნიმუშები |
| Character / Paragraph | სიმბოლო / აბზაცი |
| Character Styles / Paragraph Styles | სიმბოლოს სტილები / აბზაცის სტილები |
| Story / Story Editor | ტექსტური ნაკადი / ტექსტის რედაქტორი |
| Text Frame / Text Wrap | ტექსტური ჩარჩო / ტექსტით გარშემოვლება |
| OVERSET (frame badge) | ტექსტი არ ეტევა |
| Stroke / Fill | კონტური / შევსება |
| Bleed / Slug | ჭრისპირა არე / საინფორმაციო ზოლი |
| Preflight | ბეჭდვისწინა შემოწმება |
| Hyphenation | სიტყვების გადატანა |
| Tracking / Kerning | ტრეკინგი / კერნინგი |
| Leading / Baseline | სტრიქონთაშორისი ინტერვალი / საბაზისო ხაზი |
| Change Case / UPPERCASE | რეგისტრის შეცვლა / მთავრული |
| Book / Index / Table of Contents | წიგნი / ინდექსი / სარჩევი |
| Interface Language | ინტერფეისის ენა |

Please follow this table and the shared ArtCraft Georgian glossary when you add strings. Product and
format names stay as they are.

## Verification and maintenance

Add a row `("English source", "Georgian")` to `crates/ui-egui/src/i18n/ka.rs` whenever a key is added
to `i18n.rs` or the per-language tables. Keep placeholders (`{}`, `{name}`) and ellipses exactly;
strings added later fall back to English until they are translated.

`cargo test -p designcraft-ui-egui --lib i18n` checks that the Georgian catalog has no duplicate or
empty rows, keeps every placeholder and ellipsis, contains no Mtavruli, returns its rows through
`tr`, and writes counts as `noun: n`. `cargo test -p designcraft-engine change_case` covers Change
Case on Georgian text, and `style_row_menu_strings_are_translated_in_every_language` covers Georgian
with the other languages. A native-speaker skim is welcome.

## Revision history

| Date | Change | Summary |
|---|---|---|
| 2026-10-17 | minor | Catalog synced with upstream (2,370 entries); web language and font notes |
| 2026-10-13 | minor | Georgian interface notes and terminology |
