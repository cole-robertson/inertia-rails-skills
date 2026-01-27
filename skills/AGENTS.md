# Inertia Rails Skills

A comprehensive collection of agent skills for building high-quality Inertia.js applications with Ruby on Rails.

Compatible with 29+ AI coding agents via the [Vercel Skills CLI](https://github.com/vercel-labs/skills).

## Available Skills

### Core Reference

| Skill | Description | Priority |
|-------|-------------|----------|
| [inertia-rails-best-practices](inertia-rails-best-practices/SKILL.md) | Comprehensive best practices with 50+ rules across 8 categories | Reference |

### Task-Focused Skills

| Skill | Description | Use When |
|-------|-------------|----------|
| [inertia-rails-setup](inertia-rails-setup/SKILL.md) | Project setup and configuration | Creating new projects, adding Inertia to existing Rails apps |
| [inertia-rails-forms](inertia-rails-forms/SKILL.md) | Form handling and validation | Building forms, handling validation, file uploads |
| [inertia-rails-auth](inertia-rails-auth/SKILL.md) | Authentication and authorization | Login, sessions, permissions, access control |
| [inertia-rails-testing](inertia-rails-testing/SKILL.md) | RSpec and Minitest testing | Writing tests for Inertia responses |
| [inertia-rails-performance](inertia-rails-performance/SKILL.md) | Performance optimization | Code splitting, prefetching, deferred props |

## Installation

### One-Command Install (Recommended)

Using the [Vercel Skills CLI](https://github.com/vercel-labs/skills):

```bash
# Install all skills to your project
npx skills add cole-robertson/inertia-rails-skills

# Install globally (available across all projects)
npx skills add cole-robertson/inertia-rails-skills -g

# Install for specific agents only
npx skills add cole-robertson/inertia-rails-skills -a claude-code -a cursor

# List available skills before installing
npx skills add cole-robertson/inertia-rails-skills --list
```

### Manual Installation

```bash
# Clone and copy to your project
git clone https://github.com/cole-robertson/inertia-rails-skills.git
cp -r inertia-rails-skills/skills/* ~/.claude/skills/
```

## Quick Reference

### Best Practices Categories

1. **Server-Side Setup & Configuration** (CRITICAL)
   - Use Rails generator for setup
   - Configure asset versioning
   - Set up proper layouts

2. **Props & Data Management** (CRITICAL)
   - Return only necessary data
   - Use shared data for globals
   - Leverage lazy evaluation
   - Use deferred props

3. **Forms & Validation** (HIGH)
   - Use useForm helper
   - Handle validation errors properly
   - Follow PRG pattern

4. **Navigation & Routing** (HIGH)
   - Use Link component
   - Configure HTTP methods correctly
   - Handle redirects properly

5. **Performance Optimization** (MEDIUM-HIGH)
   - Implement code splitting
   - Use prefetching
   - Optimize partial reloads

6. **Security** (MEDIUM-HIGH)
   - Server-side auth
   - Pass permissions as props
   - History encryption

7. **Testing** (MEDIUM)
   - RSpec matchers
   - Minitest assertions
   - E2E with Capybara

8. **Advanced Patterns** (MEDIUM)
   - Persistent layouts
   - Custom resolvers
   - Event handling

## Frontend Framework Support

All skills support the three official Inertia.js frontend adapters:

- **React** (`@inertiajs/react`)
- **Vue 3** (`@inertiajs/vue3`)
- **Svelte** (`@inertiajs/svelte`)

Code examples are provided in Vue 3 by default, with React and Svelte alternatives where significant differences exist.

## Resources

- [Inertia Rails Documentation](https://inertia-rails.dev/)
- [Inertia.js Documentation](https://inertiajs.com/)
- [GitHub: inertiajs/inertia-rails](https://github.com/inertiajs/inertia-rails)
- [Evil Martians: Inertia.js in Rails](https://evilmartians.com/chronicles/inertiajs-in-rails-a-new-era-of-effortless-integration)

## License

MIT License
