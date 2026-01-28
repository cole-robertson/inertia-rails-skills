# Claude Instructions for Inertia Rails Skills

This file provides guidance for Claude Code on how to use the Inertia Rails skills effectively.

## When to Use These Skills

### Automatic Activation

These skills should be referenced when the user is:

- Working with Inertia.js and Ruby on Rails
- Building single-page applications with Rails backends
- Using `inertia_rails` gem
- Creating React, Vue, or Svelte frontends with Rails
- Asking about forms, navigation, or data passing in Inertia

### Trigger Phrases

Activate skills when you detect:

- "Inertia", "inertia_rails", "InertiaRails"
- "render inertia:", "inertia_share"
- "useForm", "@inertiajs"
- References to React/Vue/Svelte with Rails
- "modern monolith" architecture discussions

## Skill Usage Guidelines

### inertia-rails-best-practices

**Use for:** General guidance, code review, refactoring decisions

**Key points to emphasize:**
- Always return minimal props data (security + performance)
- Use `as_json(only: [...])` to whitelist fields
- Never expose sensitive data (password_digest, tokens, etc.)
- Use deferred props for non-critical data
- Follow the PRG pattern for form submissions

### inertia-rails-setup

**Use for:** New projects, adding Inertia to existing apps

**Recommend for NEW projects:**
1. Clone the official starter kit:
   - React: `git clone https://github.com/inertia-rails/react-starter-kit myapp`
   - Vue: `git clone https://github.com/inertia-rails/vue-starter-kit myapp`
   - Svelte: `git clone https://github.com/inertia-rails/svelte-starter-kit myapp`
2. Run `bin/setup` to install dependencies
3. Customize from there (auth, shadcn/ui, layouts included)

**For EXISTING Rails apps:**
1. Use the Rails generator: `bin/rails generate inertia:install`
2. Configure asset versioning with ViteRuby
3. Set up shared data in ApplicationController
4. Create proper initializer configuration

### inertia-rails-forms

**Use for:** Form implementation, validation, file uploads

**Key patterns:**
- Always use `useForm` helper for state management
- Handle errors with `form.errors`
- Use redirect pattern after successful submission
- Preserve scroll on validation errors
- Use error bags for multiple forms on same page

### inertia-rails-auth

**Use for:** Authentication, authorization, permissions

**Critical points:**
- Auth is handled server-side (no special OAuth needed)
- Pass permissions as props, not helpers
- Use history encryption for sensitive pages
- Clear history on logout

### inertia-rails-testing

**Use for:** Writing tests for Inertia responses

**Key matchers (RSpec):**
- `expect(inertia).to be_inertia_response`
- `expect(inertia).to render_component('path/component')`
- `expect(inertia).to have_props(key: value)`
- `expect(inertia).to have_flash(notice: 'message')`

### inertia-rails-performance

**Use for:** Optimization, slow pages, large datasets

**Optimization priorities:**
1. Minimize props data
2. Use deferred props for expensive queries
3. Implement partial reloads
4. Add prefetching for likely navigation
5. Use code splitting for large apps

## Code Review Checklist

When reviewing Inertia Rails code, check for:

### Props (CRITICAL)
- [ ] Only necessary fields returned
- [ ] No sensitive data exposed
- [ ] Using `as_json(only: [...])` or serializers
- [ ] Large datasets paginated or deferred

### Controllers
- [ ] Following redirect pattern after POST/PUT/DELETE
- [ ] Errors passed via `inertia: { errors: ... }`
- [ ] Shared data set up properly
- [ ] Authorization checked before data access

### Frontend
- [ ] Using `Link` component for navigation (not `<a>`)
- [ ] Using `useForm` for form state
- [ ] Handling `form.processing` state
- [ ] Displaying validation errors

### Performance
- [ ] Expensive queries deferred
- [ ] Partial reloads for filtered data
- [ ] Appropriate prefetching configured

## Common Mistakes to Catch

1. **Exposing entire models:**
   ```ruby
   # BAD
   render inertia: { user: User.find(id) }

   # GOOD
   render inertia: { user: User.find(id).as_json(only: [:id, :name]) }
   ```

2. **Rendering instead of redirecting after forms:**
   ```ruby
   # BAD
   render inertia: { user: @user }

   # GOOD
   redirect_to user_url(@user)
   ```

3. **Using `<a>` tags for internal links:**
   ```vue
   <!-- BAD -->
   <a href="/users">Users</a>

   <!-- GOOD -->
   <Link href="/users">Users</Link>
   ```

4. **Not handling form errors:**
   ```vue
   <!-- BAD -->
   <input v-model="form.email" />

   <!-- GOOD -->
   <input v-model="form.email" />
   <span v-if="form.errors.email">{{ form.errors.email }}</span>
   ```

## Framework-Specific Notes

### React
- Use `setData('field', value)` instead of direct assignment
- Destructure from useForm: `{ data, setData, post, errors, processing }`

### Vue 3
- Use `v-model` directly: `v-model="form.email"`
- Access via `form.errors.email`

### Svelte
- Use stores with `$form.email`
- Access errors via `$form.errors.email`

## Response Format

When explaining Inertia concepts:

1. Start with the **why** (the problem it solves)
2. Show **incorrect** approach first (if applicable)
3. Show **correct** approach with code
4. Explain **key points** to remember
5. Link to relevant documentation

## Version Compatibility

These skills target:
- `inertia_rails` gem 3.x+
- `@inertiajs/*` packages 2.x+
- Rails 7.x+
- Vite Ruby (recommended bundler)
