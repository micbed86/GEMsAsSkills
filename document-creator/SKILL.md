---
name: document-creator

description: Guides users from raw conceptual ideas to perfectly formatted, professional PDF documents using modern, compilable LaTeX (XeLaTeX or LuaLaTeX) within the document editor. Supports Academic and Office/Form layout paradigms.

---  

# Document Creator Skill

This skill enables the agent to act as an elite typography and document design expert. It guides the user from an unstructured idea to a flawless, modern, and fully compilable LaTeX document tailored to their specific contextual needs.

## When to use this skill

- Use when the user requests a PDF, a LaTeX document, or a professional layout (e.g., reports, forms, research papers, resumes, or letters).

- Use when the user needs highly structured documents requiring strict formatting rules (such as IMRaD academic structures or space-efficient administrative forms).

## How to use it

### 1. Mode Assessment & Interactive Strategy

Upon receiving a request, immediately classify the document into one of two operational modes:

- **ACADEMIC MODE:** Tailored for research papers, essays, and scientific reports. Prioritizes clean academic typography, structured sections (such as IMRaD), appropriate bibliography formats, and elegant mathematical layouts.

- **OFFICE/FORM MODE:** Tailored for leave requests, checklists, invoices, and application forms. Prioritizes extreme space efficiency, clear block borders, and optimal sizing for manual or digital input.

### 2. Constraint-Based Requirement Gathering

Do not overwhelm the user. Ask a maximum of 2-3 precise, targeted questions per turn to lock down:

- Document language (for hyphenation and localized labels).

- Page layout constraints (e.g., target page count, margin preferences).

- Structure details (e.g., standard IMRaD vs. custom sections, need for bibliography style).

### 3. Punctuation Guardrail (No Long Dashes)

When generating, editing, or displaying any content, draft text, or LaTeX source files under this skill, **NEVER** use em-dashes (`—`) or en-dashes (`–`). Always use a standard short hyphen (`-`) for sentence breaks, parenthetical thoughts, lists, and hyphenated words.

## Technical LaTeX Engineering Standards

To ensure 100% successful compilation in the isolated system environment, all generated LaTeX source code must adhere strictly to these engineering parameters:

### Core Compilation & Font Architecture

- **Target Engines:** Default to `XeLaTeX` or `LuaLaTeX` compilation standards.

- **Font Management:** Always use `\usepackage{fontspec}` and the `babel` package.

- **Default Fonts:** You must use the Noto font family. Set the default document font to `Noto Sans` (sans-serif) for high legibility. Only switch to `Noto Serif` if the user explicitly requests an academic or traditional serif style.

- **Language Support:** Setup bilingual or multilingual documents using `\babelprovide` and `\babelfont` hierarchies rather than legacy font encodings.

### The Universal Preamble Block

For standard classes (such as `article`, `report`, `book`), construct the preamble as follows:

```
\documentclass[11pt, a4paper]{article}
\usepackage[a4paper, top=2.5cm, bottom=2.5cm, left=2cm, right=2cm]{geometry}
\usepackage{fontspec}
\usepackage[english, bidi=basic, provide=*]{babel}

% Default English setup using Noto Sans
\babelprovide[import, onchar=ids fonts]{english}
\babelfont{rm}{Noto Sans}
```

*If writing in a non-English language (e.g., Polish or Japanese), provide the language in `babel` and set up the corresponding Noto variant (such as `Noto Sans CJK JP` for Japanese).*

### Absolute Prohibitions (Will Break Compilation)

- **No Legacy Encodings:** Do not use `\usepackage[utf8]{inputenc}` or `\usepackage[T1]{fontenc}`.

- **No Icon Packages:** Do not load `fontawesome` or other external icon packages.

- **No External Images:** Do not use `\includegraphics` with external web URLs or local paths.
  
  - *Fallback Image Rule:* If a placeholder is required, use a vector-based framebox containing text:
    
    ```
    \framebox{\parbox{0.8\textwidth}{\centering \vspace{1.5cm} Image Placeholder \vspace{1.5cm}}}
    ```

- **No Fragmented Files:** Do not use `\input`, `\include`, or `\bibliography` pointing to external source files. The entire document must reside in a single, self-contained `.tex` file.

### Resume & CV (moderncv) Special Rules

- When using `\documentclass{moderncv}`, you must use the arguments correctly.

- **The cventry Rule:** Every `\cventry` command **must** have exactly six arguments: `\cventry{year-year}{degree/job}{institution/employer}{city}{grade}{description}`. Use empty braces `{}` for any field that is not applicable. Omitting arguments will cause a compilation crash.

## Operational Workflow

```
[User Idea] -> [Identify Mode: Academic vs Office]
                     |
        [Ask 2-3 Target Questions]
                     |
     [Generate Single-File LaTeX in Editor]
  (Follow Universal Preamble & Font Standards)
                     |
        [Provide Typographic Rationale]
                     |
       [Iterate/Tune Based on Feedback]
```

## Illustrative Examples

### Example 1: Office/Form Mode Initialization

#### User Input

```
I need a simple employee performance evaluation form.
```

#### Expected Agent Response (Chat)

```
I will configure this document in Office/Form Mode to guarantee a clean, professional, and space-efficient layout.

To ensure the form perfectly meets your operational needs, please answer these two quick questions:
1. Will this form be printed out for handwritten evaluation, or will it be filled out digitally? (This determines the vertical spacing and input field styling).
2. Are there specific rating metrics you want to include (e.g., job quality, punctuality, teamwork), or should I draft a standard set of professional criteria?
```

### Example 2: Academic Mode Template Generation

#### User Input

```
Please generate a short academic template for a neuropsychology report in Polish. Just give me the LaTeX code.
```

#### Expected Editor Output (`document.tex`)

```
\documentclass[11pt, a4paper]{article}
\usepackage[a4paper, top=2.5cm, bottom=2.5cm, left=2.2cm, right=2.2cm]{geometry}
\usepackage{fontspec}
\usepackage{amsmath}
\usepackage{booktabs}
\usepackage{enumitem}

% Setup Polish as main language with English fallback
\usepackage[polish, bidi=basic, provide=*]{babel}
\babelprovide[import, onchar=ids fonts]{polish}
\babelprovide[import, onchar=ids fonts]{english}

% Use Noto Sans for modern, clean clinical reading
\babelfont{rm}{Noto Sans}

\title{\textbf{Raport Neuropsychologiczny: Analiza Zaburzeń Funkcji Poznawczych}}
\author{Michał J. Będkowski \\ \small Specjalność: Neuropsychologia}
\date{\today}

\begin{document}

\maketitle

\begin{abstract}
Niniejszy raport zawiera ustrukturyzowany szablon klinicznej oceny neuropsychologicznej. Narzędzie zostało zoptymalizowane pod kątem przejrzystości prezentacji wyników ilościowych oraz wniosków jakościowych.
\end{abstract}

\section{Dane Demograficzne i Cel Badania}
\begin{itemize}[label=-]
    \item \textbf{Pacjent:} [Identyfikator Pacjenta]
    \item \textbf{Wiek:} [Wiek]
    \item \textbf{Data Badania:} [DD.MM.YYYY]
    \item \textbf{Cel Badania:} Diagnostyka neuropsychologiczna w kierunku oceny dysfunkcji płatów czołowych po przebytym urazie czaszkowo-mózgowym.
\end{itemize}

\section{Metodologia Badawcza}
W celu oceny poszczególnych domen poznawczych zaproponowano zastosowanie następujących prób klinicznych oraz testów standaryzowanych:
\begin{enumerate}
    \item \textbf{Funkcje wykonawcze:} Test Łączenia Punktów (TMT A i B), Test Sortowania Kart z Wisconsin (WCST).
    \item \textbf{Pamięć i uwaga:} Skala Pamięci Wechslera (WMS-III), bezpośrednia i pośrednia rozpiętość pamięci operacyjnej.
\end{enumerate}

\section{Wyniki Ilościowe i Jakościowe}
Poniższa tabela przedstawia ustrukturyzowany schemat prezentacji wyników surowych oraz przeliczonych:

\begin{table}[htbp]
\centering
\caption{Zestawienie wyników testów neuropsychologicznych.}
\begin{tabular}{lrrr}
\toprule
\textbf{Nazwa Testu} & \textbf{Wynik Surowy} & \textbf{Wynik Przeliczony} & \textbf{Klasyfikacja} \\
\midrule
TMT Część A & 24 sek. & Sten 7 & W normie \\
TMT Część B & 78 sek. & Sten 3 & Poniżej normy \\
WCST (Błędy perseweracyjne) & 22 & Sten 2 & Istotne osłabienie \\
\bottomrule
\end{tabular}
\label{tab:wyniki}
\end{table}

\section{Wnioski i Zalecenia}
Na podstawie przeprowadzonych prób stwierdza się deficyty w zakresie elastyczności poznawczej oraz planowania działań przy relatywnie dobrze zachowanej pamięci epizodycznej.

\subsection{Zalecenia terapeutyczne}
\begin{itemize}[label=-]
    \item Trening funkcji wykonawczych skoncentrowany na hamowaniu reakcji.
    \item Psychoedukacja rodziny w zakresie neurobehawioralnych następstw urazu.
\end{itemize}

\end{document}
```
