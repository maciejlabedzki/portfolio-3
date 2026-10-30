# Project Context & Developer Guidelines

## 1. Project Overview
This repository contains a modern, high-performance personal developer portfolio. The primary purpose of this project is to showcase professional work, technical case studies, skills, and interactive demos, while providing a seamless way for recruiters and collaborators to get in touch.

### Primary Goals
- **Showcase Projects:** Detailed case studies with live links, source code, screenshots, and technical breakdowns.
- **Performance & SEO:** Fast load times, 100/100 Lighthouse score target, semantic HTML, and dynamic Open Graph metadata.
- **Accessibility (a11y):** WCAG 2.1 AA compliance, full keyboard navigation, and screen reader compatibility.
- **Responsive & Interactive:** Mobile-first approach with fluid layouts and subtle micro-interactions.

---

## 2. Tech Stack

- **Framework:** Next.js (App Router, React 18+)
- **Language:** TypeScript (Strict mode enabled)
- **Styling:** Tailwind CSS with CSS Variables for theme management
- **UI & Components:** Radix UI primitives / shadcn/ui, Lucide React (icons)
- **Animations:** Framer Motion (page transitions, micro-interactions)
- **State & Data Handling:** React hooks, Server Actions, Zod (schema validation)
- **Form Handling:** React Hook Form + Resend / EmailJS (for contact form)
- **Deployment & Hosting:** Vercel

---

## 3. Key Concepts & Architecture

### Directory Structure
```text
├── src/
│   ├── app/                 # Next.js App Router pages and layouts
│   │   ├── layout.tsx       # Root layout with metadata and theme providers
│   │   ├── page.tsx         # Home page / Hero section
│   │   └── projects/        # Project showcases and dynamic routes [slug]
│   ├── components/          # Reusable UI elements
│   │   ├── ui/              # Base primitives (buttons, inputs, dialogs)
│   │   └── sections/        # Page sections (Hero, About, Projects, Contact)
│   ├── content/             # Static or MDX data for projects/articles
│   ├── hooks/               # Custom React hooks
│   ├── lib/                 # Utility functions (cn, formatters, API clients)
│   └── types/               # TypeScript interfaces and global declarations
```

### Server vs. Client Components
- Keep components as **Server Components (RSC)** by default.
- Use `"use client"` only when client interactivity is strictly required (e.g., event listeners, hooks like `useState`/`useEffect`, Framer Motion wrappers).
- Isolate client-side logic to the leaves of the component tree.

### Theming
- System-aware Dark/Light mode using `next-themes`.
- Style elements using semantic tokens (`bg-background`, `text-foreground`, `border-border`) rather than hardcoded hex values.

---

## 4. Coding Standards

### TypeScript
- Maintain strict typing: **never use `any`**. Use `unknown` with type guards if the type is truly dynamic.
- Explicitly define interfaces or types for all component props and API responses.
- Prefer `interface` for extensible data models and `type` for unions/primitives.

### Component Structure
- Use functional components with explicit prop typing.
- Colocate small helper sub-components or utility functions when they are exclusively used within a single component.
- Example pattern:
  ```tsx
  interface ProjectCardProps {
    title: string;
    description: string;
    tags: string[];
    href: string;
  }

  export function ProjectCard({ title, description, tags, href }: ProjectCardProps) {
    return (
      <article className="rounded-lg border bg-card p-6 text-card-foreground shadow-sm">
        <h3 className="text-xl font-semibold tracking-tight">{title}</h3>
        <p className="mt-2 text-muted-foreground">{description}</p>
        <div className="mt-4 flex flex-wrap gap-2">
          {tags.map((tag) => (
            <span key={tag} className="text-xs font-medium">
              {tag}
            </span>
          ))}
        </div>
      </article>
    );
  }
  ```

### Styling & Tailwind
- Always use the `cn()` helper utility (combining `clsx` and `tailwind-merge`) when conditionally merging classes.
- Avoid inline styles.
- Organize Tailwind classes logically: layout -> spacing -> sizing -> typography -> colors -> effects/animations.

### Git & Commit Conventions
- Follow **Conventional Commits**:
  - `feat:` for new features or sections
  - `fix:` for bug fixes
  - `style:` for UI/CSS adjustments that do not alter logic
  - `refactor:` for code cleanups and restructuring
  - `chore:` for dependency updates or configuration changes
- Keep commits granular and self-contained.