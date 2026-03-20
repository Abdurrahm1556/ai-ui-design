# Component Patterns

> Copy-paste UI component patterns with HTML structure, Tailwind classes, and accessibility notes.

## Button Variants

### Standard Button Set

```html
<!-- Primary -->
<button class="inline-flex items-center rounded-lg bg-blue-600 px-4 py-2.5
  text-sm font-medium text-white shadow-sm hover:bg-blue-700
  focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2
  focus-visible:outline-blue-600 transition-colors">
  Primary Action
</button>

<!-- Secondary -->
<button class="inline-flex items-center rounded-lg bg-white px-4 py-2.5
  text-sm font-medium text-gray-700 shadow-sm ring-1 ring-inset ring-gray-300
  hover:bg-gray-50 transition-colors">
  Secondary Action
</button>

<!-- Ghost -->
<button class="inline-flex items-center rounded-lg px-4 py-2.5
  text-sm font-medium text-blue-600 hover:bg-blue-50 transition-colors">
  Text Action
</button>

<!-- Danger -->
<button class="inline-flex items-center rounded-lg bg-red-600 px-4 py-2.5
  text-sm font-medium text-white shadow-sm hover:bg-red-700 transition-colors">
  Delete
</button>
```

**Accessibility**: Always use `<button>` instead of `<div>`. Ensure `focus-visible` styles are present.

## Form Patterns

### Input with Validation

```html
<div>
  <label for="email" class="block text-sm font-medium text-gray-700">Email</label>
  <input type="email" id="email" name="email"
    class="mt-1 block w-full rounded-lg border-gray-300 shadow-sm
    focus:border-blue-500 focus:ring-blue-500 sm:text-sm"
    placeholder="you@example.com" />
</div>

<!-- Error state -->
<div>
  <label for="email-error" class="block text-sm font-medium text-gray-700">Email</label>
  <input type="email" id="email-error" aria-describedby="email-error-msg"
    class="mt-1 block w-full rounded-lg border-red-300 text-red-900
    placeholder-red-300 focus:border-red-500 focus:ring-red-500 sm:text-sm"
    value="invalid-email" />
  <p id="email-error-msg" class="mt-1 text-sm text-red-600">Please enter a valid email address</p>
</div>
```

### Loading State Button

```html
<button disabled class="inline-flex items-center rounded-lg bg-blue-600 px-4 py-2.5
  text-sm font-medium text-white opacity-75 cursor-not-allowed">
  <svg class="mr-2 h-4 w-4 animate-spin" viewBox="0 0 24 24" fill="none">
    <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4" />
    <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8v4a4 4 0 00-4 4H4z" />
  </svg>
  Submitting...
</button>
```

## Card Layouts

### Product Card

```html
<div class="group overflow-hidden rounded-xl bg-white shadow-sm ring-1 ring-gray-200
  hover:shadow-md transition-shadow">
  <div class="aspect-[4/3] overflow-hidden bg-gray-100">
    <img src="product.jpg" alt="Product name"
      class="h-full w-full object-cover group-hover:scale-105 transition-transform duration-300" />
  </div>
  <div class="p-4">
    <h3 class="text-sm font-semibold text-gray-900">Product Name</h3>
    <p class="mt-1 text-sm text-gray-500">Short description</p>
    <p class="mt-2 text-lg font-bold text-gray-900">$29.99</p>
  </div>
</div>
```

### Stat Card

```html
<div class="rounded-xl bg-white p-6 shadow-sm ring-1 ring-gray-200">
  <p class="text-sm font-medium text-gray-500">Total Revenue</p>
  <p class="mt-2 text-3xl font-bold text-gray-900">$45,231</p>
  <p class="mt-1 text-sm text-green-600">+12.5% vs last month</p>
</div>
```

## Modal Pattern

```html
<!-- Backdrop + centered dialog -->
<div class="fixed inset-0 z-50 flex items-center justify-center">
  <div class="fixed inset-0 bg-black/50" aria-hidden="true"></div>
  <div role="dialog" aria-modal="true" aria-labelledby="modal-title"
    class="relative w-full max-w-md rounded-xl bg-white p-6 shadow-xl">
    <h2 id="modal-title" class="text-lg font-semibold text-gray-900">Confirm Delete</h2>
    <p class="mt-2 text-sm text-gray-600">This action cannot be undone. Are you sure?</p>
    <div class="mt-6 flex justify-end gap-3">
      <button class="rounded-lg px-4 py-2 text-sm font-medium text-gray-700
        ring-1 ring-gray-300 hover:bg-gray-50">Cancel</button>
      <button class="rounded-lg bg-red-600 px-4 py-2 text-sm font-medium text-white
        hover:bg-red-700">Delete</button>
    </div>
  </div>
</div>
```

## Navigation Patterns

### Sidebar

```html
<nav class="flex w-64 flex-col bg-gray-900 p-4">
  <a href="#" class="flex items-center gap-3 rounded-lg bg-gray-800 px-3 py-2
    text-sm font-medium text-white">
    <svg class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
        d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3" />
    </svg>
    Home
  </a>
  <a href="#" class="flex items-center gap-3 rounded-lg px-3 py-2
    text-sm font-medium text-gray-400 hover:bg-gray-800 hover:text-white transition-colors">
    <svg class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
        d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6m6 0V9a2 2 0 012-2h2a2 2 0 012 2v10" />
    </svg>
    Analytics
  </a>
</nav>
```

### Breadcrumb

```html
<nav aria-label="Breadcrumb">
  <ol class="flex items-center gap-2 text-sm">
    <li><a href="#" class="text-gray-500 hover:text-gray-700">Home</a></li>
    <li class="text-gray-400">/</li>
    <li><a href="#" class="text-gray-500 hover:text-gray-700">Products</a></li>
    <li class="text-gray-400">/</li>
    <li class="font-medium text-gray-900" aria-current="page">Product Details</li>
  </ol>
</nav>
```

## Data Table

```html
<div class="overflow-hidden rounded-xl ring-1 ring-gray-200">
  <table class="min-w-full divide-y divide-gray-200">
    <thead class="bg-gray-50">
      <tr>
        <th scope="col" class="px-4 py-3 text-left text-xs font-medium uppercase
          tracking-wider text-gray-500">Name</th>
        <th scope="col" class="px-4 py-3 text-left text-xs font-medium uppercase
          tracking-wider text-gray-500">Status</th>
        <th scope="col" class="px-4 py-3 text-right text-xs font-medium uppercase
          tracking-wider text-gray-500">Actions</th>
      </tr>
    </thead>
    <tbody class="divide-y divide-gray-200 bg-white">
      <tr class="hover:bg-gray-50">
        <td class="whitespace-nowrap px-4 py-3 text-sm text-gray-900">Project Alpha</td>
        <td class="px-4 py-3">
          <span class="inline-flex rounded-full bg-green-100 px-2.5 py-0.5
            text-xs font-medium text-green-800">Active</span>
        </td>
        <td class="px-4 py-3 text-right text-sm">
          <button class="text-blue-600 hover:text-blue-800">Edit</button>
        </td>
      </tr>
    </tbody>
  </table>
</div>
```
