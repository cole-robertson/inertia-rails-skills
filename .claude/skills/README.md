# Inertia Rails Skills

<p align="center">
  <strong>Comprehensive Claude Code skills for building modern Rails applications with Inertia.js</strong>
</p>

<p align="center">
  <a href="#installation">Installation</a> •
  <a href="#available-skills">Skills</a> •
  <a href="#quick-start">Quick Start</a> •
  <a href="#documentation">Docs</a>
</p>

---

## What is this?

A collection of **Claude Code skills** that provide best practices, patterns, and automation for building **Inertia.js applications with Ruby on Rails**. These skills turn years of Inertia Rails expertise into reusable guidance that Claude can apply while helping you code.

Inspired by [Vercel's agent-skills](https://github.com/vercel-labs/agent-skills) for React/Next.js, this package provides equivalent comprehensive coverage for the Inertia Rails ecosystem.

## Features

- **50+ Best Practices** organized by priority and impact
- **8 Categories** from setup to advanced patterns
- **Multi-Framework Support** for React, Vue 3, and Svelte
- **Task-Focused Skills** for forms, auth, testing, and performance
- **Code Examples** with incorrect vs. correct patterns
- **Automated Setup** script for new projects

## Installation

### Quick Install (Recommended)

```bash
# Clone or download the skills
git clone https://github.com/your-repo/inertia-rails-skills.git

# Copy to your project
cp -r inertia-rails-skills/.claude/skills/* /path/to/your/project/.claude/skills/

# Or install globally for all projects
cp -r inertia-rails-skills/.claude/skills/* ~/.claude/skills/
```

### Manual Installation

1. Create the skills directory in your project:
   ```bash
   mkdir -p .claude/skills
   ```

2. Copy the skill folders:
   ```bash
   cp -r inertia-rails-best-practices .claude/skills/
   cp -r inertia-rails-setup .claude/skills/
   cp -r inertia-rails-forms .claude/skills/
   cp -r inertia-rails-auth .claude/skills/
   cp -r inertia-rails-testing .claude/skills/
   cp -r inertia-rails-performance .claude/skills/
   ```

## Available Skills

### Core Reference Skill

| Skill | Description |
|-------|-------------|
| **[inertia-rails-best-practices](inertia-rails-best-practices/SKILL.md)** | Comprehensive guide with 50+ rules across 8 categories, prioritized by impact. The main reference for all Inertia Rails development. |

### Task-Focused Skills

| Skill | Description | When to Use |
|-------|-------------|-------------|
| **[inertia-rails-setup](inertia-rails-setup/SKILL.md)** | Project setup and configuration | New projects, adding Inertia to existing Rails apps |
| **[inertia-rails-forms](inertia-rails-forms/SKILL.md)** | Form handling with useForm, validation, uploads | Building forms, handling errors, file uploads |
| **[inertia-rails-auth](inertia-rails-auth/SKILL.md)** | Authentication and authorization patterns | Login flows, Devise integration, permissions |
| **[inertia-rails-testing](inertia-rails-testing/SKILL.md)** | RSpec and Minitest testing | Writing tests for Inertia responses |
| **[inertia-rails-performance](inertia-rails-performance/SKILL.md)** | Performance optimization techniques | Code splitting, prefetching, deferred props |

## Quick Start

### 1. Set Up a New Inertia Rails Project

Ask Claude Code:
> "Set up a new Rails project with Inertia and React"

Or invoke the skill directly:
```
/inertia-rails-setup react --typescript --tailwind
```

### 2. Build Forms with Validation

Ask Claude Code:
> "Create a user registration form with validation"

Claude will use the forms skill to implement proper patterns with useForm, error handling, and the PRG (Post-Redirect-Get) pattern.

### 3. Add Authentication

Ask Claude Code:
> "Add Devise authentication with Inertia login pages"

The auth skill provides patterns for session management, permission passing, and history encryption.

### 4. Write Tests

Ask Claude Code:
> "Write RSpec tests for this Inertia controller"

The testing skill includes all RSpec matchers and Minitest assertions for Inertia responses.

## Best Practices Categories

The skills organize 50+ rules into 8 priority-ranked categories:

| Priority | Category | Impact |
|----------|----------|--------|
| CRITICAL | Server-Side Setup | Foundation for all functionality |
| CRITICAL | Props & Data Management | 2-5× performance, security |
| HIGH | Forms & Validation | User experience, data integrity |
| HIGH | Navigation & Routing | SPA experience |
| MEDIUM-HIGH | Performance | 30-70% faster loads |
| MEDIUM-HIGH | Security | Protection against vulnerabilities |
| MEDIUM | Testing | Code quality |
| MEDIUM | Advanced Patterns | Scalability |

## Example Rules

### Props Management (CRITICAL)

**Incorrect:**
```ruby
def show
  render inertia: { user: User.find(params[:id]) }
  # Exposes all columns including password_digest!
end
```

**Correct:**
```ruby
def show
  user = User.find(params[:id])
  render inertia: {
    user: user.as_json(only: [:id, :name, :email, :avatar_url])
  }
end
```

### Deferred Props (HIGH)

```ruby
def dashboard
  render inertia: {
    # Critical data - loads immediately
    user: current_user.as_json(only: [:id, :name]),

    # Non-critical - loads after initial render
    analytics: InertiaRails.defer { Analytics.expensive_query },
    recommendations: InertiaRails.defer(group: 'extras') { compute_recommendations }
  }
end
```

### Authorization Props (HIGH)

```ruby
def index
  render inertia: {
    can: { create_user: allowed_to?(:create?, User) },
    users: User.all.map do |user|
      user.as_json(only: [:id, :name]).merge(
        can: {
          edit: allowed_to?(:edit?, user),
          delete: allowed_to?(:destroy?, user)
        }
      )
    end
  }
end
```

## Frontend Framework Support

All skills support the three official Inertia.js adapters:

| Framework | Package | Status |
|-----------|---------|--------|
| React | `@inertiajs/react` | Full support |
| Vue 3 | `@inertiajs/vue3` | Full support |
| Svelte | `@inertiajs/svelte` | Full support |

Examples are primarily in Vue 3, with React/Svelte alternatives where patterns differ significantly.

## Documentation

- **[AGENTS.md](AGENTS.md)** - Index of all skills
- **[Best Practices Reference](inertia-rails-best-practices/references/AGENTS.md)** - Complete rules with examples

### External Resources

- [Inertia Rails Documentation](https://inertia-rails.dev/)
- [Inertia.js Documentation](https://inertiajs.com/)
- [GitHub: inertiajs/inertia-rails](https://github.com/inertiajs/inertia-rails)
- [Evil Martians: Inertia.js in Rails](https://evilmartians.com/chronicles/inertiajs-in-rails-a-new-era-of-effortless-integration)

## Directory Structure

```
.claude/skills/
├── README.md                           # This file
├── AGENTS.md                           # Skills index
├── CLAUDE.md                           # Claude-specific instructions
│
├── inertia-rails-best-practices/       # Main reference skill
│   ├── SKILL.md                        # Skill definition
│   ├── README.md                       # Skill documentation
│   ├── references/
│   │   └── AGENTS.md                   # 50+ detailed rules
│   └── scripts/
│       └── setup.sh                    # Setup automation
│
├── inertia-rails-setup/                # Setup skill
│   └── SKILL.md
│
├── inertia-rails-forms/                # Forms skill
│   └── SKILL.md
│
├── inertia-rails-auth/                 # Auth skill
│   └── SKILL.md
│
├── inertia-rails-testing/              # Testing skill
│   └── SKILL.md
│
└── inertia-rails-performance/          # Performance skill
    └── SKILL.md
```

## Contributing

Contributions welcome! Areas for improvement:

- Additional best practices and patterns
- More framework-specific examples (React, Svelte)
- Integration with other Rails gems
- Edge case handling and troubleshooting guides

## Acknowledgments

- [Vercel agent-skills](https://github.com/vercel-labs/agent-skills) for the skill structure inspiration
- [Inertia.js](https://inertiajs.com/) and [Jonathan Reinink](https://twitter.com/reinink) for creating Inertia
- [Evil Martians](https://evilmartians.com/) for the inertia_rails gem maintenance
- The Rails and Inertia communities

## License

MIT License - see [LICENSE](LICENSE) for details.
