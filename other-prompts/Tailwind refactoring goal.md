# Refactoring Goal

This is a stand-alone html file as a high quality prototype for a React application homepage. The file must remain self contained. 

## Our Goal
Our goal is to refactor your homepage to align with Tailwind CSS v3 best practices, focusing on centralised theming and reducing custom CSS. We’re doing this step-by-step to transform your hybrid approach (mixing custom CSS with Tailwind) into a utility-first workflow that fully leverages Tailwind’s strengths, while preparing for a proper setup (e.g., with a tailwind.config.js file) to manage themes centrally.

## Why We’re Doing This
By aligning with Tailwind’s best practices, we aim to:
- Streamline Development: Minimise context-switching between HTML and CSS.
- Prepare for Centralised Theming
- Improve Scalability: Make the code more maintainable and simple
- Optimise Performance: Eventually replace the CDN with a build process to purge unused styles.

## What Are Tailwind Best Practices?
Broadly, Tailwind CSS v3 best practices revolve around:
- Utility-First Approach: Use Tailwind’s pre-defined utility classes (e.g., `p-4`, `bg-blue-500`) in HTML instead of writing custom CSS, reserving custom styles for edge cases.
- Centralised Configuration: Define design tokens (colours, fonts, spacing) in `tailwind.config.js` for consistency and easy theme management.
- Responsive and State-Driven Design: Leverage Tailwind’s modifiers (e.g., `md`:, `hover`:) for responsiveness and interactivity without media queries or custom selectors.
- Minimal Custom CSS: Only use custom CSS for complex layouts or effects that utilities can’t handle, often with `@apply` in a build setup.
- Build Optimisation: Use a build process (not CDN) to generate lean, production-ready CSS by removing unused styles.

By reducing custom CSS in this step, we’re laying the groundwork for these practices, with centralised theming as the next big win.