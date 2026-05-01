# 🎨 Tailwind CSS for Rails: Design System

[![ClawHub Skill](https://img.shields.io/badge/ClawHub-Skill-blue)](#) [![Agent Skill](https://img.shields.io/badge/Agent-Skill-blue)](#)

**Consistent, Dark-Mode-Ready UI Components for Ruby on Rails ERB Views.**

This documentation provides a standardized library of Tailwind CSS utility patterns and ERB implementation strategies. The goal is to maintain a unified design language across all Rails applications, ensuring that every component—from badges to complex tables—is responsive, accessible, and natively supports dark mode.

---

## 🚀 The Core Utility: `cn()`

To prevent "class soup" and messy conditional logic in your ERB templates, the foundation of this design system is the `cn()` helper. This helper flattens, de-duplicates, and cleans up CSS class strings.

### Implementation

Add this to your `app/helpers/application_helper.rb`:

```ruby
# app/helpers/application_helper.rb
def cn(*classes)
  classes.flatten.compact.join(' ').split.uniq.join(' ')
end
```

### Usage in ERB

Use it to cleanly toggle classes based on object state:

```erb
<%# Clean, readable conditional logic %>
<div class="<%= cn('px-4 py-2 transition-colors', active ? 'bg-blue-500 text-white' : 'bg-gray-100 text-gray-900') %>">
  <%= active ? 'Active State' : 'Inactive State' %>
</div>
```

---

## 🧩 Standardized Components

### 1. The Badge Pattern

Use these for status indicators (Success, Warning, Error, Info). Always include both light and dark mode color pairs.

| Status | Light Mode | Dark Mode |
| :--- | :--- | :--- |
| **Success** | `bg-green-100 text-green-800` | `dark:bg-green-900 dark:text-green-100` |
| **Warning** | `bg-yellow-100 text-yellow-800` | `dark:bg-yellow-900 dark:text-yellow-100` |
| **Error** | `bg-red-100 text-red-800` | `dark:bg-red-900 dark:text-red-100` |
| **Info** | ` ...blue... ` | ` ...blue... ` |

**Code Snippet:**

```erb
<span class="inline-flex items-center rounded-full px-3 py-1 text-sm font-medium bg-green-100 text-green-800 dark:bg-green-900 dark:text-green-100">
  Verified
</span>
```

### 2. The Surface Card

Standardized container for content blocks, featuring a subtle border and depth.

```erb
<div class="rounded-lg border border-gray-20 $ dark:border-gray-800 bg-white dark:bg-gray-950 shadow-sm">
  <div class="p-6">
    <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Card Title</h3>
    <p class="text-gray-600 dark:text-gray-400">Card description text goes here.</p>
  </div>
</div>
```

### 3. Responsive Data Tables

A wrapper designed to handle overflow on mobile devices while maintaining a professional shadow and ring.

```erb
<div class="overflow-hidden shadow ring-1 ring-black ring-opacity-5 md:rounded-lg">
  <table class="min-w-full divide-y divide-gray-300 dark:divide-gray-800">
    <thead class="bg-gray-50 dark:bg-gray-900">
      <!-- Table Headers -->
    </thead>
    <tbody class="divide-y divide-gray-200 dark:divide-gray-800">
      <!-- Table Rows -->
    </tbody>
  </table>
</div>
```

---

## 📐 Design Principles & Best Practices

To maintain the integrity of this design system, all developers (and agents) should adhere to the following rules:

### 🟢 Always Do

* **Mobile-First:** Always write base classes for mobile, then use `sm:`, `md:`, and `lg:` prefixes to scale up.
* **Dual-Mode Pairs:** Every color utility should be accompanied by its `dark:` counterpart (e.g., `bg-white dark:bg-gray-950`).
* **Partial Extraction:** If a component is used more than twice, extract it into a partial (eg. `_button.html.erb`).
* **Semantic Coloring:** Use color to convey meaning (Green = Success, Red = Error).

### 🔴 Never Do

* **Never use "Class Soup":** Avoid long, unreadable strings of classes in your ERB; always use the `cn()` helper for logic.
* **Never ignore contrast:** Ensure that your `dark:text-gray-400` is readable against `dark:bg-gray-950`.
* **Never skip the `cn()` helper:** Do not manually concatenate strings with `+` or `#{}` without the helper, as it leads to messy whitespace and duplicate classes.

---

## 🔗 Related Documentation

* **[Component Library](./references/components.md)**: Full library of shared partials (Buttons, Modals, Inputs).
* **[Dark Mode & Responsiveness](./references/dark-mode-responsive.md)**: Advanced CSS architecture and breakpoint strategies.

---
**Original implementation by [@djc00p](https://github.com/djc00p)**
