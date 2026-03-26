# LaTeX Academic Template
This is a **LaTeX Engineering Template** built on the "Convention over Configuration" philosophy. Its core objective is to achieve **hierarchical isolation**, enabling the seamless migration and rapid reuse of academic assets (figures, tables, algorithms, and text) across different publisher templates.


## 📂 Project Structure
This project treats paper construction as an automated pipeline where each layer handles specific tasks, ensuring the decoupling of content and presentation.

```bash
# 1. Raw Assets Layer
├── assets/                 # Original experimental data (SVG, AI, Python Plots, Excel)
│
# 2. LaTeX Adaptation Layer (Component Bridge)
├── components/             # Bridge: Wraps Assets into LaTeX-callable objects
│   ├── figures/            # Independent .tex snippets containing \includegraphics, \caption, \label
│   ├── tables/             # Encapsulated table logic
│   └── algorithms/         # Encapsulated pseudocode blocks
│
# 3. Semantic Contents Layer
├── contents/               # Pure text content, independent of specific typesetting styles
│   ├── modules/            # Body of the paper (Chapters or Sections)
│   ├── appendix/           # Appendix content
│   ├── references/         # Bibliography database (.bib)
│   └── structure.tex       # Logical organization layer; arranges the Modules 
│
# 4. Environment Config Layer
├── configs/                # Global package dependencies and custom macros
│
# 5. Presentation/Output Layer
├── main.tex                # Entry point for publisher templates (e.g., IEEEtran.cls / nature.cls)
│
# 6. Support & Ops Layer
├── scripts/                # Automation scripts (data-to-table conversion, cleanup, etc.)
└── backups/                # Fault-tolerance: Backups of old versions for Git-unfamiliar collaborators
```


## 🌟 Core Philosophy
### Convention over Configuration
By utilizing a preset folder structure, there is no need to write complex path-finding logic in `main.tex`. As long as files are placed in their corresponding `modules` or `components` directories, they can be called via standardized `\input` commands, significantly reducing configuration overhead during environment migrations.

### Modular Isolation
The neutral naming of `contents/modules` refers to either `sections` or `chapters`:
- **Short Papers/Conferences**: A Module corresponds to a `\section`.
- **Long Papers/Theses**: A Module corresponds to a `\chapter`.

### Bridge Layer Design
This is the essence of the template. `components` acts as a bridge between `assets` and `contents`:
- **Modification-Friendly**: If an image needs to be swapped from `.pdf` to `.png`, you only need to modify the wrapper code in `components` without touching the actual body text in `contents`.
- **Multi-Invoke**: The same figure component can be referenced simultaneously by the thesis `main.tex` and a presentation `beamer.tex`.

### Collaborative Compatibility
Acknowledging that not all academic collaborators are proficient with Git, the `backups` folder provides a physical storage space for older drafts or "scratchpads" revised by collaborators, ensuring manual fault tolerance during version rollbacks.


## 💡 Usage Guide
1.  **Prepare Material**: Place raw experimental figures/plots into `assets`.
2.  **Create Components**: Create corresponding `.tex` files in `components` that reference the exported files in `assets`.
3.  **Draft Content**: Complete the narrative in `contents/modules`, referencing the components from `components` where necessary.
4.  **Inject into Container**: Assemble the entire paper in `main.tex` via `\input{contents/structure.tex}`.


## 🚀 Rapid Submission Switching
When you need to switch target journals, your workflow requires only two steps:
1.  **Replace `main.tex`**: Use the `.cls` and `.tex` samples provided by the publisher.
2.  **Redirect References**: In the new `main.tex`, re-mount your content assets via `\input{configs/...}` and `\input{contents/structure.tex}`.


## 🔗 Related Projects
In addition to this LaTeX template, I have developed an academic template based on **Typst**: [Typst-Academic-Template](https://github.com/yuliu625/Yu-Typst-Academic-Template). While Typst is a more modern and efficient typesetting tool, LaTeX remains the dominant standard in academia. You can:
- Use Typst for daily writing and rapid content construction.
- Use relevant tools to convert Typst projects to LaTeX format. (This works well for solo papers; collaborative papers may still require shared LaTeX online editing tools.)

The purpose of this template series is to enable easy conversion and reuse of content across different typesetting tools to adapt to various collaboration and submission requirements.

