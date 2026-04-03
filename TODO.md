# Boneyard Angular Port - TODO

## Project Overview
Porting the Boneyard skeleton loading framework from React to Angular 19, with full @defer block support for zero-layout-shift lazy loading.

## Phase 1: Fork & Setup
- [x] Fork 0xGF/boneyard to davidRamirez90/boneyard-angular
- [ ] Create `packages/boneyard-angular` directory structure
- [ ] Copy core TypeScript files (non-React specific):
  - `extract.ts` - DOM snapshot logic
  - `layout.ts` - Layout computation
  - `runtime.ts` - Bone rendering
  - `types.ts` - TypeScript interfaces
  - `responsive.ts` - Breakpoint handling

## Phase 2: Core Angular Components
- [ ] Create `BoneyardSkeletonComponent`:
  - `@Input() name: string` - skeleton identifier
  - `@Input() loading: boolean` - toggle skeleton/real content
  - `@Input() color: string` - bone fill color (default: #e0e0e0)
  - `@Input() animate: boolean` - pulse animation toggle
  - `@ContentChild()` or `ng-content` for real content projection
  - Lifecycle hooks: `ngOnInit`, `ngOnChanges`, `ngAfterViewInit`
  
- [ ] Create `BoneyardService` (DI registry):
  - `registerBones(name: string, bones: SkeletonResult)`
  - `getBones(name: string): SkeletonResult | null`
  - `resolveResponsive(bones, width)` - breakpoint matching
  - Use Angular DI instead of global Map

- [ ] Create `BoneyardRegistryLoader`:
  - APP_INITIALIZER provider
  - Load `.bones.json` files at bootstrap
  - Register all skeletons with BoneyardService

## Phase 3: @defer Integration
- [ ] Test with Angular 19 @defer blocks:
  ```html
  @defer (on viewport) {
    <app-heavy-component />
  } @placeholder {
    <boneyard-skeleton name="heavy-component" />
  }
  ```
- [ ] Ensure skeleton dimensions match deferred component exactly
- [ ] Handle responsive skeletons with ResizeObserver or window:resize
- [ ] Test breakpoint switching (mobile → tablet → desktop)

## Phase 4: CLI Integration
- [ ] Verify CLI works with Angular dev server:
  ```bash
  npx boneyard-js build http://localhost:4200
  ```
- [ ] Add npm script to package.json:
  ```json
  "scripts": {
    "bones:build": "boneyard-js build http://localhost:4200 --out ./src/assets/bones"
  }
  ```
- [ ] Document CLI usage for Angular projects

## Phase 5: Angular-Specific Features
- [ ] Signals integration for reactive breakpoint updates:
  ```typescript
  currentBreakpoint = computed(() => resolveBreakpoint(windowWidth()))
  ```
- [ ] Standalone component support (Angular 19 default)
- [ ] OnPush change detection optimization
- [ ] Support for Angular Material theming (optional)

## Phase 6: Testing & Documentation
- [ ] Unit tests for BoneyardService
- [ ] Component tests for BoneyardSkeletonComponent
- [ ] Integration test with @defer block
- [ ] Create README with:
  - Installation instructions
  - Quick start guide
  - @defer usage examples
  - Comparison with ngx-skeleton-loader
  
## Phase 7: Internal Release
- [ ] Publish to internal npm registry (if available)
- [ ] Or use git submodule/subtree approach
- [ ] Share with team (3 frontend devs, 4 backend devs)
- [ ] Gather feedback for iteration

## Nice to Have (Future Phases)
- [ ] Angular schematic for `ng add boneyard-angular`
- [ ] SSR (Server-Side Rendering) support for bones
- [ ] Animation customization (CSS variables)
- [ ] Integration with Angular CDK overlay for modals
- [ ] Browser extension for visual skeleton editing

## Resources
- Original repo: https://github.com/0xGF/boneyard
- Angular @defer docs: https://angular.dev/guide/defer
- ngx-skeleton-loader (existing solution): https://github.com/willmendesneto/ngx-skeleton-loader

## Team Context
- Project: Angular 19 migration
- Current e2e: Broken (needs better loading states)
- Target: Kubernetes for development
- Docs need: Business logic documentation from code
- Team: 3 frontend, 4 backend devs
