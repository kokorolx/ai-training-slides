---
title: Training Proposal — Advanced AI for Developers
date: 2026-05-21
---

Hi anh,

Dạo này AI có khá nhiều cập nhật lớn về cách làm việc — không chỉ là "hỏi đáp" nữa mà đã có thể làm việc theo kiểu agent, tự động hóa nhiều bước liên tiếp. Em muốn xin đề xuất 1 buổi training nội bộ nhỏ (~3–4 tiếng) để chia sẻ với team cách tận dụng những thứ này hiệu quả hơn trong công việc hàng ngày.

**Outline dự kiến:**

**1. Memory System** *(~50 phút)*
- 1.1. 7 Levels of AI Usage — mình đang ở đâu, cần đến đâu
- 1.2. CLAUDE.md là gì — project memory cho AI
- 1.3. 5 rules viết CLAUDE.md hiệu quả từ production
- 1.4. Before / After: làm việc không có vs có memory
- 1.5. Cross-session memory — AI nhớ qua nhiều buổi làm việc ra sao
- 1.6. Exercise: viết CLAUDE.md cho repo mình đang làm

**2. Skills & Slash Commands** *(~45 phút)*
- 2.1. Skill là gì — thay vì nhắc AI mỗi lần, viết 1 lần dùng mãi
- 2.2. Anatomy của một skill tốt
- 2.3. Demo: `/brainstorming` — explore trước khi code
- 2.4. Demo: `/systematic-debugging` — quy trình debug có kỷ luật
- 2.5. Red flags: khi nào AI hay bỏ qua workflow
- 2.6. Exercise: draft skill cho task lặp lại nhất của bạn

**3. Agents & Orchestration** *(~45 phút)*
- 3.1. Agent vs Chatbot — sự khác biệt thực sự
- 3.2. opsx pipeline: propose → apply → review → archive
- 3.3. `/opsx:apply` — bước agentic là gì, chạy ra sao
- 3.4. Demo thực tế: refactor feature trên codebase NUS
- 3.5. `.agents/` folder — team memory, không phải personal
- 3.6. Exercise: vẽ agent workflow diagram cho 1 feature đang làm

**4. MCP — Kết nối AI với tooling thật** *(~45 phút)*
- 4.1. MCP là gì — Model Context Protocol, nguyên lý hoạt động
- 4.2. Ecosystem hiện tại: Datadog, Linear, Amplitude, DB, Slack...
- 4.3. Demo: daily health check chỉ bằng 1 lệnh
- 4.4. Demo: cross-tool query — thứ chỉ possible khi có MCP
- 4.5. Cách đề xuất / tích hợp MCP tool mới cho team
- 4.6. Exercise: list 3 MCP tools bạn muốn có

**Wrap-up** *(~15 phút)*
- Mỗi người mang về: CLAUDE.md · skill draft · agent diagram · MCP backlog
- Roadmap sau training: Week 1 → 2 → 3–4 → 5+

Em có thể chuẩn bị slide sẵn, anh thấy có phù hợp không ạ?

---

## Training 2 — Spec-Driven Development *(~3 tiếng)*

> Buổi này tập trung vào **lý thuyết và tư duy**: tại sao cần spec trước khi code, flow làm việc chuẩn trông như thế nào, và khảo sát các tool hiện có. Buổi sau sẽ đào sâu thực hành từng tool.

---

### Core loop (áp dụng cho cả 3 tools)

```
Idea → Brainstorm → Spec → Tasks + AC → Code → Verify → Ship
         (explore)  (what)   (how)               (evidence)
```

**Nguyên tắc nền tảng:**
- Không code trước khi design được approve — hard gate, không exception
- Spec = thoả thuận giữa người và AI về "done" trông như thế nào
- AC (Acceptance Criteria) = câu hỏi có thể trả lời được bằng Yes/No
- Verification = chạy evidence thật, không tự claim xong

---

**1. Vấn đề cần giải quyết** *(~20 phút)*
- 1.1. Context rot là gì — AI càng làm nhiều thì output càng tệ dần
- 1.2. Vicious cycle: fix nhanh → mất context → fix sai → fix thêm
- 1.3. "Vibe coding" vs spec-driven: khi nào dùng cái nào
- 1.4. Chi phí thực của việc không có spec: rework, misalignment, regression

**2. Spec-Driven Flow — Lý thuyết** *(~30 phút)*
- 2.1. Brainstorm phase: explore intent trước khi commit vào bất kỳ hướng nào
- 2.2. Proposal: WHAT & WHY — không phải HOW
- 2.3. Design / Specs: kiến trúc, data model, API contract, edge cases
- 2.4. Tasks: bite-sized, mỗi task tự verify được độc lập
- 2.5. AC (Acceptance Criteria): "feature done" = tất cả AC = Yes
- 2.6. Verification gate: evidence trước khi claim complete
- 2.7. Archive: đóng loop, knowledge persist cho lần sau

**3. Khảo sát 3 tools** *(~40 phút)*

*3.1. OpenSpecs (`/opsx`)*
- Flow: `propose` → `specs` → `design` → `tasks` → `apply` → `archive`
- Artifacts: proposal.md · specs.md · design.md · tasks.md — tất cả file, không volatile
- Khi nào dùng: feature mới, refactor lớn, API contract change
- Demo: `/opsx:propose` cho 1 ticket Linear thật

*3.2. Superpowers (`/brainstorming` + `/writing-plans`)*
- Flow: explore → clarify questions → 2–3 approaches → design doc → plan → execute
- Hard gate: AI không được code trước khi user approve design
- Anti-pattern: "this is too simple to need a design" — mọi task đều cần
- Khi nào dùng: khi cần AI tư duy cùng mình trước khi viết 1 dòng code

*3.3. Get Shit Done (`/gsd`)*
- Flow: `new-project` → `discuss-phase` → `plan-phase` → `execute-phase` → `verify-work` → `ship`
- Context isolation: mỗi phase chạy trong fresh 200k-token context — không bị context rot
- Shared artifacts: PROJECT.md · ROADMAP.md · STATE.md persist qua session
- Quality gates: plan verification trước execute, acceptance testing trước ship
- Khi nào dùng: project lớn nhiều phase, cần parallelization, cần quality gate chặt

*3.4. So sánh nhanh*

| | OpenSpecs | Superpowers | GSD |
|---|---|---|---|
| Scope | Per-change | Per-task | Per-project/phase |
| Artifact | proposal/specs/design/tasks | design doc + plan | PROJECT/ROADMAP/STATE |
| Context mgmt | Manual | Manual | Tự động (fresh context/phase) |
| Tốt nhất cho | Feature spec | Collaborative design | Multi-phase project |

**4. Deep dive: Get Shit Done** *(~50 phút)*
- 4.1. Tại sao GSD — context rot problem và cách GSD giải quyết
- 4.2. PROJECT.md — "nguồn sự thật" duy nhất cho toàn project
- 4.3. ROADMAP.md — phases, goals, dependencies
- 4.4. `/gsd-discuss-phase` — capture decisions trước khi plan (quan trọng nhất)
- 4.5. `/gsd-plan-phase` — AI research + tạo PLAN.md + tự verify plan
- 4.6. `/gsd-execute-phase` — wave-based parallelization, fresh context per task
- 4.7. `/gsd-verify-work` — conversational UAT, AI tự test feature
- 4.8. Demo end-to-end: 1 phase thật từ discuss → ship
- 4.9. Exercise: map 1 Linear ticket hiện tại vào GSD flow

**5. Khi nào dùng tool nào** *(~15 phút)*
- 5.1. Decision tree: task size × risk level → chọn tool
- 5.2. Tiny task (1–2h): vibe coding OK, không cần spec
- 5.3. Normal task (nửa ngày): Superpowers brainstorm + opsx
- 5.4. Feature lớn / multi-repo: GSD với phases
- 5.5. Kết hợp: GSD phases + opsx per-change trong mỗi phase

**Wrap-up** *(~15 phút)*
- Mỗi người mang về: decision tree in ra dán bàn · 1 ticket đang làm map vào GSD flow
- Preview buổi sau: thực hành live trên repo thật với GSD end-to-end
