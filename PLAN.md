# My_Profile — Portfolio & Repository Normalization Plan

**Repository:** `SlncTrZ/SlncTrZ`
**Workspace:** `/mnt/pc-dev/My_Profile`
**Updated:** 2026-09-06

## 1. Goal

Biến GitHub profile thành trang đại diện đúng cho năng lực hiện tại của SlncTrZ, đồng thời chuẩn hóa branch/push policy để contribution graph và snake phản ánh đúng khối lượng phát triển thực tế.

North star:

> Local-first AI infrastructure + production systems + robotics/UAV + embedded/lighting engineering.

Profile không nên trông như một tập hợp demo AI rời rạc. Nó phải thể hiện khả năng xây infrastructure, ship product và kết nối software với hệ thống vật lý.

## 2. Featured project hierarchy

Thứ tự flagship hiện tại:

1. **SlncTrZ-MCP** — Universal AI Capability Gateway
2. **Ebook_Transalator** — Agentic Translation Workbench
3. **ArtNetController** — Professional DMX / Art-Net Controller
4. **AI-Apps** — AI Production Factory
5. **MeiLin_Project** — Embodied Digital Intelligence
6. **UAV_FLyingwing** — Edge-AI UAV Platform

Nhóm Labs / Specialized Systems:

- AI_DMX_Autopilot
- Forex-AI
- Slnc_Pi
- Local LLM fine-tuning / QLoRA / GGUF workflows

### Rule

Chỉ đưa một project lên Featured khi có ít nhất một trong các bằng chứng sau:

- runtime thực tế;
- release/package chạy được;
- test/CI evidence;
- hardware/field evidence;
- architecture khác biệt rõ;
- product workflow hoàn chỉnh.

Không xếp fork ngang hàng với original repository nếu phần lớn lịch sử thuộc upstream.

## 3. SlncTrZ-MCP — flagship policy

`SlncTrZ-MCP` là flagship số 1.

Canonical branch:

```text
main
├── feat/*
├── fix/*
├── refactor/*
└── vX.Y.Z tags
```

### Current state

Audit trực tiếp ngày 2026-09-06:

- `main` là canonical branch và GitHub remote HEAD/default branch.
- Remote hiện chỉ còn `main`; legacy `dev` và `master` đã được xóa.
- Local `main` đang tracking `origin/main` và đồng bộ tại release `v0.2.4` (`7a63bcc`).
- Repo có CI workflow, standalone workflow, `ARCHITECTURE.md`, release documentation và tags `v0.2.0` → `v0.2.4`.
- Release mới tiếp tục dùng tag `v*` từ canonical `main` history.

### Required action

1. giữ `main` là canonical/default branch duy nhất;
2. không tái tạo disconnected `master`/squash-only release history;
3. xác nhận contribution graph phản ánh đúng history `main`;
4. dùng tag `v*` từ `main` cho mọi release mới;
5. nâng public evidence bằng architecture diagram, Owner Console screenshot và CI/release badges.

## 4. Repository branch standard

### Original repositories

Mặc định:

```text
main = canonical development + GitHub default branch
```

Feature/fix branch phải ngắn hạn và merge về `main`.

### Legacy repositories hiện còn `master`

Đã tạo `main` song song cho:

- AI-Apps
- OmniVoice
- Slnc_VideoAdapter
- Slnc_Pi

Audit trực tiếp ngày 2026-09-06:

| Repo | Remote default | `main` vs `master` | Local state | Migration risk |
| --- | --- | --- | --- | --- |
| AI-Apps | `master` | cùng commit `a04f790` | `master`, dirty | thấp sau khi worktree sạch |
| OmniVoice | `master` | cùng commit `825ac00` | `master`, dirty | thấp sau khi worktree sạch |
| Slnc_VideoAdapter | `master` | cùng commit `69a147d` | `master`, dirty | thấp sau khi worktree sạch |
| Slnc_Pi | `master` | **đã diverge** (`main=ba7cba6`, `master=b92ab6d`) | `master`, dirty và behind upstream | **cao — phải reconcile history trước khi đổi default** |

Không rename/switch local cưỡng bức khi worktree còn dirty. Riêng `Slnc_Pi` không được áp dụng migration cơ học; phải xác định canonical history và reconcile `main`/`master` trước.

Migration sequence cho từng repo:

1. hoàn tất/commit các thay đổi đang dở;
2. fetch `origin/main`;
3. verify `main` chứa đúng canonical history;
4. switch local sang `main`;
5. set upstream `origin/main`;
6. đổi GitHub Default branch sang `main`;
7. kiểm tra CI/scripts/docs không còn hard-code `master`;
8. chỉ xóa `master` sau khi xác nhận không có deployment/release dependency.

### Forks

Fork có thể giữ branch convention của upstream để giảm friction. `Odysseus` hiện có thể tiếp tục theo `dev` upstream workflow.

## 5. Git transport policy

Các repo SlncTrZ trên development host sử dụng SSH origin:

```text
git@github.com:SlncTrZ/<repo>.git
```

Mục tiêu:

- fetch/push không phụ thuộc HTTPS credential helper;
- consistent behavior giữa repo;
- tránh local commit bị tồn đọng vì push thất bại im lặng.

## 6. Contribution graph & Snake

Snake chỉ mirror dữ liệu contribution GitHub; nó không tự đọc commit local.

Một commit có thể không xuất hiện nếu:

- chưa push lên GitHub;
- nằm lâu trên non-default branch;
- canonical history chưa reachable từ default branch;
- author/email không được GitHub account nhận diện;
- repository/private contribution setting không cho hiển thị.

### Snake workflow

Workflow hiện tại:

- chạy mỗi 6 giờ;
- quyền tối thiểu `contents: write`;
- light/dark SVG;
- concurrency guard;
- commit SVG chỉ khi graph thay đổi.

### Verification routine

Khi nghi contribution bị thiếu:

1. `git status -sb`;
2. kiểm tra `ahead/behind` với upstream;
3. verify author/email;
4. verify GitHub default branch;
5. kiểm tra commit có reachable từ default branch;
6. query GitHub public contribution graph;
7. chỉ debug snake workflow sau khi các bước trên đều đúng.

## 7. README profile roadmap

### Phase A — Completed

- [x] SlncTrZ-MCP lên vị trí flagship #1.
- [x] Bỏ hierarchy cũ Qwen/MovieMaker-first.
- [x] Thêm AI-Apps, MeiLin vào Featured.
- [x] Tách Labs & Specialized Systems.
- [x] Viết lại Engineering Domains.
- [x] Snake hỗ trợ dark/light theme.
- [x] Tăng refresh cadence snake.

### Phase B — Repository normalization

- [x] GitHub Default branch `SlncTrZ-MCP`: `master → main`; remote `dev/master` đã xóa.
- [x] Audit live branch/default state của 4 repo legacy (2026-09-06).
- [ ] GitHub Default branch `AI-Apps`: `master → main`.
- [ ] GitHub Default branch `OmniVoice`: `master → main`.
- [ ] GitHub Default branch `Slnc_VideoAdapter`: `master → main`.
- [ ] Reconcile history `Slnc_Pi` trước, sau đó mới quyết định `master → main`.
- [ ] Sau khi từng worktree sạch, switch local các repo legacy sang canonical `main`.
- [ ] Audit toàn bộ CI/workflow/docs hard-code branch names.
- [ ] Xác nhận contribution graph sau migration.

### Phase C — Portfolio evidence

Audit artifact hiện có ngày 2026-09-06 (số test bên dưới là **file hiện diện**, không phải claim test đang PASS):

| Project | Evidence đã thấy trong repo | Gap cần đưa lên public profile |
| --- | --- | --- |
| SlncTrZ-MCP | `ci.yml`, `standalone.yml`, 247 test files, `ARCHITECTURE.md`, release docs, tags đến `v0.2.4` | architecture diagram/screenshot + CI/release badges |
| Ebook Translator | `windows-native.yml`, `WINDOWS_RELEASE.md`, 31 test files | packaged-app screenshot + public release/tag evidence |
| ArtNetController | `build.yml`, `assets/DMXMaster.png`, architecture/release/build docs, 9 test files | audit stale version/link + ảnh UI/hardware thực tế + clean working state |
| AI-Apps | architecture ở các capability/subproject, VMK visual assets | thiếu repo-level CI/evidence summary; cần factory diagram |
| MeiLin | `ci.yml`, architecture docs, virtual/3D assets, 20 test files | digital-twin/demo capture có thể đánh giá trong 30–60 giây |
| UAV | `test.yml`, architecture docs, modeling photos, 20 test files | CAD/telemetry/SITL hoặc flight-test evidence rõ ràng |

Actions:

- [ ] SlncTrZ-MCP: thêm architecture diagram / Owner Console screenshot / CI badge / release badge.
- [ ] Ebook Translator: thêm packaged-app screenshot và release/tag evidence.
- [ ] ArtNetController: dọn README version/link cũ, thêm ảnh UI/hardware thực tế.
- [ ] AI-Apps: thêm diagram factory → capabilities → production domains và repo-level evidence summary.
- [ ] MeiLin: thêm digital-twin/demo evidence.
- [ ] UAV: thêm CAD, telemetry, simulation hoặc flight-test evidence.

### Phase D — Profile polish

- [ ] Rà broken links của toàn bộ Featured Projects.
- [ ] Chuẩn hóa naming/casing (`Ebook_Transalator` nếu giữ tên repo thì mô tả vẫn dùng “Ebook Translator”).
- [ ] Giảm badge không cần thiết.
- [ ] Ưu tiên evidence hơn marketing claim.
- [ ] Kiểm tra README render trên GitHub desktop + mobile + light/dark mode.

## 8. Quality rules

Profile và project README phải tuân theo:

1. **No inflated claims** — chỉ nói “production-ready”, “verified”, “X tests passing” khi có evidence hiện tại.
2. **Originality visible** — original repo phải nổi bật hơn fork/vendor-derived repo.
3. **Evidence over volume** — demo, CI, release, benchmark, hardware evidence quan trọng hơn số commit/file.
4. **No stale infrastructure details** — không đưa private host/IP/path nội bộ lên public profile nếu không cần thiết.
5. **No stale links** — repository names, release URLs và badges phải được audit định kỳ.
6. **Canonical branch consistency** — mọi original active repo hướng tới `main` làm default branch.
7. **No disconnected release history** — dùng tag từ canonical history thay vì squash-only branch riêng.

## 9. Definition of Done

Portfolio normalization được coi là hoàn tất khi:

- `SlncTrZ-MCP` và các original active repo chính dùng `main` làm GitHub default;
- local upstream tracking khớp remote;
- không còn unpushed completed commits do transport/config lỗi;
- contribution graph phản ánh đúng các ngày làm việc chính;
- snake refresh tự động và không phải debug thủ công;
- README Featured Projects phản ánh đúng thứ tự flagship;
- mỗi Featured Project có evidence đủ mạnh để người ngoài đánh giá trong khoảng 30–60 giây;
- profile không chứa project/link stale hoặc claim không còn đúng.

## 10. Immediate next actions

1. Hoàn tất/commit hoặc chủ động phân loại các worktree dirty trước khi branch migration.
2. Với `AI-Apps`, `OmniVoice`, `Slnc_VideoAdapter`: sau khi sạch, verify lại `main == master`, đổi GitHub default sang `main`, rồi switch local/upstream.
3. Với `Slnc_Pi`: audit divergence `main`/`master`, chọn canonical history và reconcile trước mọi default-branch change.
4. Audit CI/workflow/docs hard-code `master` trên 4 repo legacy.
5. Kiểm tra lại contribution ngày 2026-09-02 và các ngày migration sau khi GitHub re-index.
6. Nâng evidence theo ROI: SlncTrZ-MCP + Ebook Translator trước; sau đó ArtNetController + AI-Apps; MeiLin/UAV khi có demo/field evidence đủ mạnh.
