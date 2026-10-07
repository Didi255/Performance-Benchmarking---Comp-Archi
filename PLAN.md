# Performance Benchmarking Project Plan

**CS2053 Computer Architecture | Group of 5**
Repo: https://github.com/Didi255/Performance-Benchmarking---Comp-Archi

> This is the main guide for the project. Read all of it once, then follow your own section in **Part 6**.
> If anything changes (a device, a tool, a date), update this file and tell the group.

---

## 0. Quick summary

| Item | Decision |
|---|---|
| **Main comparison (required)** | **At least 3 laptops**. Ideally all 5 members benchmark their own laptop. |
| **Comparison across device types (bonus)** | 1 laptop from the main group + 1 tablet + 1 phone, tested with the same tools that work on all three. |
| **Benchmarks (3 main)** | Geekbench 6 · Cinebench 2024 · 3DMark (Time Spy) |
| **Supporting tools** | Speedometer 3.0 (browser), CrystalDiskMark (storage), CPU-Z / GPU-Z / HWiNFO64 (specs, clocks, temperatures, power), Windows battery report |
| **Deliverables** | Report (PDF) · Presentation slides · Live presentation (10–15 min) + Q&A (10 min) |
| **Deadlines** | Report: **27 Oct, 11:59 pm** · Presentation & viva: **28 Oct** (⚠️ the brief says 2024. Confirm this year's dates.) |

### Things still to confirm with the lecturer (M1 to ask, Week 1)
- [ ] Dates for this year's report and presentation.
- [ ] Is our design OK? Main comparison = laptops; comparison across types (phone/tablet) = bonus/additional insight.
- [ ] Report format: PDF? Page limit? Does it go through Moodle?

---

## 1. How we're marked (and where each mark comes from)

| Criterion | Weight | Main owner | What gets full marks |
|---|---|---|---|
| Selecting benchmarks & evaluation criteria | 10% | M1 | Clear reasons for each tool; what each score measures and how it's calculated |
| Device selection & specification | 5% | Everyone (M2 compiles) | Full spec table: OS, CPU, GPU, RAM, storage, display, battery |
| Description of the experiments | 10% | M1 | A procedure someone else could repeat: conditions, runs, versions |
| Results / Findings | 20% | M2 | Clean tables + charts, median of 3 runs, error/variation shown |
| Analysis | 20% | M2 + M3 + M4 | Explain **why** results differ, using architecture concepts |
| Additional experiments / insights / recommendations | 5% | M5 | Throttling, battery, power modes, comparison across device types, recommendations |
| Report quality | 10% | M2 (editor) | Consistent formatting, figures labelled, references cited |
| Presentation quality | 10% | M4 (slides lead) | Clean slides, good timing, smooth handovers |
| Q&A | 10% | **Everyone** | Every member can answer questions on **any** section |

**Tasks from the brief** (all must appear in both the report and the slides):
1. Describe the measures of performance used in each benchmark → **M1**
2. Compare results per device, pick the best overall with justification → **M2**
3. Compare our results with publicly available benchmarks → **M3**
4. Compare cost and pick the best performance for the cost, justified by use case (gaming, content creation, etc.) → **M4**
5. Additional experiments / insights / recommendations → **M5**

---

## 2. Devices

Fill this in during Week 1. Use short IDs everywhere (file names, CSV, charts).

### Group A: Laptops (main comparison, need ≥3)
| ID | Owner | Model | CPU | GPU (integrated / dedicated) | Approx. price tier |
|---|---|---|---|---|---|
| L1 | M1 – ______ | | | | |
| L2 | M2 – ______ | | | | |
| L3 | M3 – ______ | | | | |
| L4 | M4 – ______ | | | | |
| L5 | M5 – ______ | | | | |

> Variety helps the analysis: ideally a gaming laptop with a dedicated GPU, a thin/light laptop, an Intel vs an AMD machine, and an older or budget laptop.
> If two members have the same model, keep both. Two units of the same model show how much results vary between units (a useful insight).
> **If anyone has a MacBook, tell M1 in Week 1.** Tools work differently on macOS (Geekbench and Cinebench are fine; 3DMark Time Spy is Windows-only).

### Group B: Comparison across device types (bonus)
| ID | Owner | Model | Type |
|---|---|---|---|
| T1 | ______ | | Tablet |
| P1 | ______ | | Phone |
| L? | (the laptop from Group A that we pick to compare) | | Laptop |

> Whoever owns T1 and P1 runs the benchmarks on them. M5 coordinates and analyses this comparison.

---

## 3. Tools

### Main benchmarks (laptops)
| Tool | What it measures | Where to get it |
|---|---|---|
| **Geekbench 6** | CPU single-core & multi-core (real-world workloads); GPU compute (OpenCL / Vulkan) | geekbench.com (free version uploads results online) |
| **Cinebench 2024** | CPU rendering performance, single-core & multi-core (Redshift renderer); sustained load | Maxon website / Microsoft Store (free) |
| **3DMark: Time Spy** | DirectX 12 gaming: Graphics score, CPU score, overall score, FPS | Steam (free version, "3DMark Demo") |

### Supporting tools
| Tool | Purpose |
|---|---|
| **Speedometer 3.0** | Browser responsiveness, i.e. everyday use (https://browserbench.org/Speedometer3.0/) |
| **CrystalDiskMark** | Storage: sequential & random read/write (MB/s) |
| **HWiNFO64** | Logs CPU/GPU temperature, clock speed and **power (W)** during tests (needed for throttling analysis) |
| **CPU-Z / GPU-Z** | Exact CPU, RAM (speed, **single vs dual channel**), GPU specs |
| **`powercfg /batteryreport`** | Battery design capacity vs current capacity (Wh) → battery health |

### Used for the comparison across device types (phone/tablet/laptop)
Geekbench 6 · **3DMark Wild Life Extreme** (also has a free Stress Test on phones/tablets) · Speedometer 3.0. All three run on phones, tablets and laptops.

> ⚠️ **M1 checks in Week 1:**
> 1. Time Spy is included in the free Steam version of 3DMark.
> 2. Wild Life Extreme is available in the free Windows version, for the comparison across device types. If not, use **Steel Nomad Light**. Last fallback: **GFXBench** (free on all platforms; use the offscreen tests).
> 3. Cinebench 2024's GPU test only supports some GPUs (NVIDIA RTX / Apple / some AMD). Note which laptops can run it. It's optional.

**Everyone uses the exact same app versions.** M1 records them in [Part 4.3](#43-what-to-record).

---

## 4. Standard testing procedure (EVERYONE must follow this exactly)

This section is our "Description of the experiments" (10%). If we test inconsistently, our results can't be compared.

### 4.1 Before testing
1. **Do not update Windows or drivers during the project.** Pause Windows Update for 2–3 weeks (Settings → Windows Update → Pause). Record the Windows build and GPU driver version.
2. Laptop **plugged in** and fully charged.
3. **Power settings:**
   - Windows: Settings → System → Power → Power mode = **Best performance**.
   - If your laptop has a manufacturer app (Armoury Crate, Lenovo Vantage, MSI Center, HP Omen/Command Center, Dell Power Manager), set it to its **performance mode**.
   - **Write down which mode you used.**
4. **Restart**, then wait **10 minutes** (Windows runs startup tasks after booting).
5. Close all apps, including those in the system tray (OneDrive, Discord, Steam downloads, antivirus scans). No browser tabs except Speedometer when running it.
6. Wi-Fi **on** (Geekbench needs it to upload), no downloads.
7. Put the laptop on a **hard flat table** (not a bed or lap), nothing blocking the vents, normal room, no fan or AC blowing directly on it. Note the room temperature roughly.
8. Start **HWiNFO64** (sensors-only mode) in the background. M5 will explain logging.

### 4.2 Running the benchmarks
Run each test **3 times**, with a **5-minute cool-down** between runs.

| Order | Test | Settings | Record |
|---|---|---|---|
| 1 | Speedometer 3.0 | **Chrome** (record the version) | Score |
| 2 | Geekbench 6 CPU | Default | Single-core, multi-core, **result link** |
| 3 | Geekbench 6 GPU (Compute) | **OpenCL**, and select the **dedicated GPU** from the dropdown if you have one | Score, **result link** |
| 4 | CrystalDiskMark | Default (5 runs, 1 GiB, C: drive) | SEQ1M Q8T1 read/write, RND4K Q1T1 read/write |
| 5 | Cinebench 2024: **CPU (Single Core)** | Settings → Minimum test duration = **Off** | Score (pts) |
| 6 | Cinebench 2024: **CPU (Multi Core)** | Minimum test duration = **Off** | Score (pts) |
| 7 | 3DMark **Time Spy** | Default | Overall score, Graphics score, CPU score, Graphics test 1 & 2 FPS |
| 8 | 3DMark **Wild Life Extreme** (only for the laptop used in the comparison across types) | Default | Score, avg FPS |

> Lightest test first, heaviest last, so heat from one test doesn't affect the next.
> If your 3 runs differ by more than **5%** from each other, do **2 more runs** and note it.
> **Laptops with 2 GPUs (integrated + dedicated):** make sure the test runs on the dedicated GPU (3DMark shows the GPU used on the results screen; check it).
> The long Cinebench runs (10 and 30 min) are part of M5's throttling experiment. Do them on a separate day or after a long cool-down.

### 4.3 What to record
- **A screenshot of every result screen.** Name it like this: `L1_cinebench-multi_run1.png`
- Geekbench result links (sign in to a Geekbench Browser account so they're easy to find).
- Fill in the shared results file (`data/results.csv`) **the same day** you test.
- App versions, Windows build, GPU driver version, power mode, room temperature, date.

### 4.4 Device specification
Each member fills in a spec file for their laptop: `devices/L1.md` (template below).
Get the information from: CPU-Z, GPU-Z, HWiNFO, `msinfo32`, `powercfg /batteryreport`, the manufacturer's spec page, and Notebookcheck (cite the URLs).

```markdown
# L1 — <Brand & full model name, e.g. ASUS TUF Gaming A15 FA507NV>
- Owner: <name, index no>
- OS & build: (e.g. Windows 11 Home 23H2, build 22631.xxxx)
- CPU: (model, cores = P-cores + E-cores, threads, base/boost clock, cache L2/L3, process node, TDP)
- iGPU: (model)
- dGPU: (model, VRAM, max power/TGP in W)   ← or "none"
- RAM: (size, DDR4/DDR5, speed in MT/s, single or dual channel ← check CPU-Z Memory tab)
- Storage: (model, size, NVMe PCIe Gen3/Gen4, or SATA)
- Display: (size, resolution, refresh rate)
- Battery: (design capacity Wh, current full charge Wh, health % = current/design)
- Cooling: (number of fans, heat pipes if known)
- Weight:
- Purchase year, launch price & current price:
- Spec source links:
```

---

## 5. How the data is organised (repo layout)

```
/PLAN.md                     ← this file
/devices/L1.md ...           ← spec sheet per device (each owner)
/data/results.csv            ← ALL benchmark numbers (everyone adds their own rows)
/data/public_results.csv     ← public benchmark numbers (M3)
/data/prices.csv             ← prices + evidence links (M4)
/data/extra/                 ← throttling logs, battery, power-mode data (M5)
/evidence/screenshots/L1/    ← benchmark screenshots per device
/evidence/prices/            ← price screenshots (M4)
/analysis/                   ← spreadsheet or Python notebook + exported charts (M2)
/report/                     ← report drafts + final PDF
/slides/                     ← presentation
/references.md               ← every source we use (everyone adds to it)
```

### `data/results.csv` format (one row per run per metric)
```csv
device_id,device_type,tool,tool_version,test,metric,run,value,unit,date,notes
L1,laptop,Geekbench 6,6.3.0,CPU,single_core,1,2450,points,2026-10-11,Best performance + Turbo mode
L1,laptop,Geekbench 6,6.3.0,CPU,multi_core,1,11200,points,2026-10-11,
L1,laptop,Geekbench 6,6.3.0,GPU OpenCL,score,1,98000,points,2026-10-11,RTX 4060 Laptop
L1,laptop,Cinebench,2024.1,CPU Single,score,1,105,pts,2026-10-11,
L1,laptop,Cinebench,2024.1,CPU Multi,score,1,890,pts,2026-10-11,
L1,laptop,3DMark,2.x,Time Spy,graphics_score,1,10200,points,2026-10-11,
L1,laptop,3DMark,2.x,Time Spy,cpu_score,1,9800,points,2026-10-11,
L1,laptop,Speedometer,3.0,Chrome 129,score,1,22.5,points,2026-10-11,
L1,laptop,CrystalDiskMark,8.0.5,SEQ1M Q8T1,read,1,4800,MB/s,2026-10-11,
```
*(Numbers above are only examples of the format.)*

### Git rules
- Each member edits **only their own files/rows** to avoid merge conflicts (the shared CSV: add rows, don't edit other people's).
- `git pull` before you start, commit often with clear messages (`Add L3 cinebench results`).
- Put screenshots into the repo, but **not videos or huge files**. HWiNFO logs (CSV) are fine.
- If you're unsure about Git, upload to the shared Drive folder and tell M2. They'll commit it.

---

## 6. Member guides

> **Each member does two kinds of work:**
> - **(A) Common work:** benchmark your own laptop following Part 4, fill in your spec file, upload screenshots + CSV rows. Owners of the phone/tablet also run the tests for the comparison across types.
> - **(B) Your own section:** described below.
>
> Each member also writes their report section(s), makes their slides, and presents them.

---

### 👤 M1: Benchmark Selection & Methodology Lead
**Covers:** Task 1 · "Selecting benchmarks & evaluation criteria" (10%) · "Description of the experiments" (10%)

**What you do**
1. **Week 1, first 2 days (others are waiting on you):**
   - Confirm the open questions in [Part 0](#things-still-to-confirm-with-the-lecturer-m1-to-ask-week-1) with the lecturer.
   - Install all tools on your laptop, do one test run of each, and check the 3 warnings in Part 3.
   - Record the **exact versions** (Geekbench, Cinebench, 3DMark, CrystalDiskMark, Chrome) and post them in the group chat. Everyone must use the same versions.
   - Create `data/results.csv` (with the header), the `devices/` template, and the folder structure in the repo.
2. **Research each benchmark in depth (Task 1).** For each tool write:
   - **What it measures:** which hardware parts it stresses (CPU cores, cache, memory, GPU, storage).
   - **How the score is built:**
     - *Geekbench 6:* runs short real-world workloads (file compression, navigation, HTML5 browser, PDF rendering, photo library, Clang compile, text processing, asset compression, object detection, background blur, horizon detection, object remover, HDR, photo filter, ray tracing, structure-from-motion). Scores are relative to a **baseline of 2500 = Intel Core i7-12700**. Multi-core uses a "shared task" model (all cores cooperate on one task, like real apps), so it doesn't grow linearly with core count. The GPU Compute score measures GPGPU performance via OpenCL/Vulkan. **Short bursts**, so it mostly shows **peak** performance, not sustained performance.
     - *Cinebench 2024:* renders a 3D scene using Maxon's **Redshift** engine (used in professional 3D work). Score in **pts**. Single-core = 1 thread; Multi-core = all threads. With the minimum duration setting it repeats the render for 10 min, so it can show **sustained** performance and throttling. Heavy floating-point/SIMD work; sensitive to core count, clock speed, cooling and power limits.
     - *3DMark Time Spy:* **DirectX 12** gaming benchmark rendered at **2560×1440**. Two graphics tests → **Graphics score** (from average FPS); one physics/CPU test → **CPU score**. The overall score is a **weighted harmonic mean**, weighted heavily towards graphics (check UL's technical guide and cite it). Represents gaming performance.
     - *Speedometer 3.0:* simulates user actions in real web apps (to-do lists, text editors, charts, news sites built with React, Vue, Angular, etc.). Higher = more responsive. Depends on single-thread CPU speed, memory latency **and** the browser's JavaScript engine.
     - *CrystalDiskMark:* sequential (large files) vs random 4K (small files, e.g. OS/app loading) read/write in MB/s.
   - **Unit** (points / pts / fps / MB/s) and whether **higher or lower is better**.
   - **Synthetic vs real-world:** classify each tool. **Peak vs sustained:** which tool shows which.
   - **Why we chose this combination:** free, they cover different parts (CPU short bursts, CPU sustained, GPU/gaming, everyday web, storage), each has a large public results database (needed for Task 3), and some run on phones/tablets too (needed for the comparison across types).
   - **Limitations:** short tests hide throttling, some workloads are tuned for particular vendors, results depend on drivers/power modes, browser engines differ.
3. **Write the testing procedure.** Turn Part 4 into a clear "Experimental Setup" section with a flow diagram (prepare → run order → 3 runs → record). Also explain *why* each control exists. For example: "plugged in + Best performance, because laptops cut power limits on battery", or "wait 10 min after boot, because background indexing uses CPU".
4. **Data quality check (Week 2, day 1):** go through `results.csv` and check everyone has 3 runs, correct units, screenshots, versions, power mode noted, dGPU used. Chase anyone missing data.

**Report sections you write:** 1. Introduction · 2. Benchmark Selection & Measures of Performance (Task 1) · 4. Experimental Methodology
**Slides (~2.5 min):** Intro/objectives · tools & what they measure · testing procedure
**Be ready to answer:** *Why these tools? Geekbench vs Cinebench: what's different? What does a Geekbench score of 2500 mean? How is the Time Spy score calculated? Synthetic vs real-world benchmarks? Why 3 runs and the median? Why plugged in and Best performance?*

---

### 👤 M2: Results & Data Analysis Lead (+ Report Editor)
**Covers:** Task 2 · "Results/Findings" (20%) · part of "Analysis" (20%) · "Device specification" (5%) · Report quality (10%)

**What you do**
1. **Build the analysis spreadsheet or notebook** (`analysis/`). Google Sheets is fine; Python (pandas + matplotlib) is better if you're comfortable with it.
   - Read `results.csv` → for each device/metric calculate the **median**, **mean**, **standard deviation**, and **coefficient of variation** (CV = SD/mean × 100%).
2. **Device spec table:** combine everyone's `devices/*.md` into one comparison table (one column per laptop). Highlight the differences that matter: core count, boost clock, TDP, dGPU and its wattage, RAM channel mode, SSD generation.
3. **Charts** (labelled axes, units, same colour for each laptop on every chart):
   - Grouped bars: Geekbench single vs multi, Cinebench single vs multi
   - Bars: Geekbench GPU, Time Spy graphics & CPU scores, Speedometer, storage (seq + random)
   - Error bars showing the range of the 3 runs
   - **Radar/spider chart** of normalised scores per laptop (good for slides)
4. **Normalised overall score** (to choose the best device):
   - For each metric: `normalised = device_score / best_score_in_group × 100`
   - Metrics: GB single, GB multi, GB GPU, Cinebench single, Cinebench multi, Time Spy graphics, Time Spy CPU, Speedometer, storage (seq read).
   - **Overall score = geometric mean** of the normalised metrics.
   - Explain **why geometric mean**: it isn't dominated by one large metric, and the ranking stays the same whichever device we use as the reference (this is the SPEC method).
   - Also show **CPU score** (GB + Cinebench) and **GPU score** (GB GPU + Time Spy graphics) separately. A laptop can win one and lose the other.
5. **Pick the best overall laptop (Task 2)** and **justify it with architecture reasons**, not just "bigger number". Use the spec table:
   - Single-core → core architecture/generation, boost clock, cache size
   - Multi-core → P-cores vs E-cores, threads, **power limit (TDP, PL1/PL2)** and cooling
   - GPU → integrated vs dedicated, GPU generation, VRAM, **GPU power (TGP)**
   - Memory → **dual vs single channel** (single channel can cut iGPU performance a lot), DDR4 vs DDR5
   - Storage → NVMe Gen4 vs Gen3 vs SATA
   - Point out **bottlenecks**, e.g. "L4 has a strong CPU but its integrated GPU limits gaming", or "L2's Cinebench multi score drops between runs → thermal limit".
6. **Report editor (Week 3):** merge everyone's sections into one document. Use the same fonts and heading styles, number figures and tables, write a table of contents, make sure every figure is referred to in the text, check references are cited ([1], [2]...). Export to PDF.

**Report sections you write:** 3. Devices & Specifications · 5. Results · 6.1 Performance Comparison & Best Device (Task 2)
**Slides (~3 min):** Device specs · results charts · overall ranking + best laptop
**Be ready to answer:** *Why geometric mean? Why does the single-core ranking differ from multi-core? What's the bottleneck of laptop X? Why does a laptop with more cores lose in Cinebench?*

---

### 👤 M3: Public Benchmark Comparison Lead
**Covers:** Task 3 · part of "Analysis" (20%)

**What you do**
1. **For every laptop we tested** (and the phone + tablet), find public results for the **same CPU/GPU, and ideally the same laptop model**:
   - **Geekbench Browser** (browser.geekbench.com): search the exact model/CPU, take the **median of many results** (10+ entries) or the official processor chart value. Save the links.
   - **Notebookcheck** (best source for laptops): their reviews and CPU/GPU pages list Cinebench 2024, Time Spy and Geekbench scores for specific laptop models.
   - **Cinebench 2024**: Notebookcheck, CPU-Monkey, Tom's Hardware CPU reviews.
   - **3DMark Time Spy**: UL's results search (3dmark.com/search), Notebookcheck GPU pages (laptop GPUs vary a lot by wattage, so compare like with like).
   - **Speedometer 3.0 / storage**: tech reviews, the SSD manufacturer's rated speeds.
   - User reviews (Amazon, Reddit, etc.) for real-world comments on heat, noise and battery. Use these as secondary evidence only.
2. Fill `data/public_results.csv`:
   ```csv
   device_id,tool,metric,our_median,public_value,source_name,source_url,date_accessed
   ```
3. Calculate the **% difference** = `(ours − public) / public × 100` for each.
4. **Chart:** our score vs public score side by side for each laptop.
5. **Explain the differences** (this is the most important part, worth Analysis marks):
   - **Power limits:** the same CPU/GPU is configured with different TDP/TGP in different laptop models (e.g. an RTX 4050 at 45 W vs 115 W)
   - **Cooling, dust and age:** older laptops with dusty fans or dry thermal paste throttle earlier
   - **Room temperature:** Sri Lankan room temperature is higher than review labs
   - **Power mode / manufacturer mode** used by the reviewer vs us
   - **RAM configuration:** single vs dual channel, RAM speed
   - **Drivers, BIOS, Windows version**, background processes
   - **Statistical:** public numbers are averages over many units, and each unit varies a little ("silicon lottery")
6. Conclude: are our results **reliable**? (e.g. "within ±5% for 4 of 5 laptops → our method is valid; L3 is −15% because of single-channel RAM").
7. Add every source to `references.md` (title, site, URL, date accessed).

**Report sections you write:** 6.2 Comparison with Public Benchmarks (Task 3)
**Slides (~2.5 min):** Our vs public chart · explanation of the differences · reliability conclusion
**Be ready to answer:** *Why are your results lower than online? Why do two laptops with the same GPU score differently? Which source is more trustworthy? How do you know your results are valid?*

---

### 👤 M4: Cost & Value Analysis Lead (+ Slides Lead)
**Covers:** Task 4 · "best price/performance ratio" · part of "Analysis" · Presentation quality (10%)

**What you do**
1. **Prices with evidence** for every laptop (save in `evidence/prices/`, list in `data/prices.csv`):
   - **Current new price in Sri Lanka**: screenshot from local sellers (e.g. Daraz, Singer, Abans, Redline, Barclays, Nanotek, official stores) **with the date visible**.
   - **Launch price** (official / press release / Notebookcheck).
   - If a laptop is no longer sold new: the **used price** from ikman.lk (state that it's used), or the closest current equivalent model.
   - If only a USD price exists: convert using the **CBSL exchange rate** on a stated date.
   ```csv
   device_id,price_lkr,price_type(new/used/launch),source,url,date_accessed,screenshot_file
   ```
2. **Price/performance metrics** (get the medians from M2):
   - Points per 10,000 LKR for each benchmark, e.g. `Cinebench multi / (price/10000)`
   - **Overall value score** = M2's overall score / price
   - Chart: **scatter plot of price (x) vs overall score (y)**. Laptops above the trend line are good value.
3. **Use-case analysis (required by the brief):** create weighted scores for each use case using the normalised scores:

   | Use case | Weights (suggested; discuss as a team and justify) |
   |---|---|
   | **Gaming** | Time Spy graphics 50% · Time Spy CPU 15% · GB GPU 15% · Cinebench sustained/stability 20% |
   | **Content creation** (3D rendering, video & photo editing) | Cinebench multi 35% · GB multi 20% · GB GPU 25% · Storage 20% |
   | **Student / office / everyday** | GB single 25% · Speedometer 30% · Battery life 35% · Storage random 10% |

   - For each use case: best **performance**, and best **performance per rupee**. These may be different laptops. Say so and explain why.
   - Explain **why** each weight was chosen (e.g. games depend mostly on the GPU; students need battery life more than raw power). Weight and portability can be mentioned as non-benchmark factors.
4. **Final answer to "which device has the best price/performance ratio?"** Give one clear overall answer + the use-case answers.
5. **Slides lead:** create the slide template in Week 2 (one clean theme, same chart style as M2). Collect everyone's slides, keep the deck to **12–15 minutes**, add title slide + **contribution slide with names & index numbers**, and run the rehearsals.

**Report sections you write:** 6.3 Cost & Price/Performance Analysis (Task 4)
**Slides (~2.5 min):** Price table with evidence · price vs performance scatter · use-case recommendations
**Be ready to answer:** *Why these weights? Why is the most expensive laptop not the best value? Where did prices come from? Which laptop would you buy for budget gaming / for a CS student?*

---

### 👤 M5: Additional Experiments & Comparison Across Device Types Lead
**Covers:** "Additional experiments / insights & recommendations" (5%) · part of "Analysis" · battery measures required by the brief

**What you do**
1. **Experiment A: Thermal throttling / sustained performance (all laptops)**
   - Cinebench 2024 CPU (Multi Core) with **Minimum test duration = 30 minutes** (or 10 min if short on time), plugged in, Best performance mode.
   - Run **HWiNFO64 logging** during the test (Sensors → "Start logging" → CSV). Log: CPU package temperature, average P-core clock, CPU package power (W).
   - Owners run it on their own laptop and send you the Cinebench screenshot + HWiNFO CSV. You compile and analyse.
   - Charts: **clock speed and temperature over time** for each laptop; first-run score vs 30-min score → **% sustained**.
   - Insight: peak vs **sustained** performance. A laptop that wins a short benchmark may lose a long render or gaming session. Link this to cooling design and power limits (PL2 boost for a short time → drops to PL1).
2. **Experiment B: On battery vs plugged in (all laptops)**
   - Run Geekbench 6 CPU + Cinebench multi + Time Spy **on battery** (same power mode) → % drop vs the plugged-in medians.
   - Insight: many laptops (especially gaming ones) cut CPU/GPU power on battery.
3. **Experiment C: Power modes (2–3 laptops)**
   - Cinebench multi in **Balanced** vs **Best performance** (and manufacturer Silent vs Performance mode if available) → score, power (W), temperature, fan noise (rough).
   - Calculate **performance per watt** = score / average package power.
4. **Experiment D: Battery life (all laptops), same test for all**
   - Charge to 100%, unplug, Balanced mode, brightness **50%**, volume 0, Wi-Fi off, keyboard backlight off.
   - Play the **same 1080p video** (one file, shared by M5) fullscreen on loop for **60 minutes**.
   - Record the battery % drop → estimated life = `60 / drop% × 100` minutes. Also record battery health from `powercfg /batteryreport` (full charge capacity / design capacity).
   - Note the limitation: 50% brightness is a different number of nits on each screen, and older batteries hold less charge.
5. **Experiment E: Comparison across device types (laptop vs tablet vs phone)**
   - Run Geekbench 6 (CPU + GPU), 3DMark Wild Life Extreme and Speedometer 3.0 on L?, T1 and P1 (the owners run their own device).
   - On the phone and tablet, also run the free **Wild Life Extreme Stress Test** (20 loops → stability %), and compare with the laptop's Cinebench sustained %.
   - Compare: single-core, multi-core, GPU, web, sustained performance, battery life.
   - Explain using architecture concepts:
     - **Power & thermal limits:** phone ~5–8 W, tablet ~8–15 W, laptop 15–100+ W → sustained performance
     - **ARM vs x86** designs, big.LITTLE / hybrid (P-core + E-core) designs
     - **Mobile GPU vs laptop iGPU/dGPU**
     - **Memory** (LPDDR vs DDR, bandwidth) and **storage** (UFS vs NVMe)
     - Different graphics APIs (Metal / Vulkan / DirectX). Discuss whether the comparison is fair.
     - Why a flagship phone's single-core score can match a laptop, but not in sustained multi-core workloads
6. **Recommendations & conclusion:** what to buy for each type of user, practical tips (performance mode when plugged in, cleaning dust from fans, dual-channel RAM upgrade), and what we learned about benchmarking (limitations; improvements such as more runs, temperature-controlled room, a wall power meter).
7. **Q&A coordinator:** collect the question bank (Part 9) and run the mock Q&A sessions in Week 3.

**Report sections you write:** 7. Additional Experiments · 8. Comparison Across Device Types · 9. Recommendations & Conclusion
**Slides (~2.5 min):** Throttling chart · battery & power-mode results · laptop vs tablet vs phone · recommendations
**Be ready to answer:** *Why does performance drop over 30 minutes? What are PL1/PL2? Why does the laptop lose performance on battery? What is performance per watt? Is comparing a phone with a laptop fair?*

---

## 7. Report structure

| # | Section | Owner | Target length |
|---|---|---|---|
| — | Title page, group members & index numbers, table of contents | M2 | 1–2 pages |
| 1 | Introduction & objectives | M1 | ½ page |
| 2 | Benchmark selection & measures of performance (**Task 1**) | M1 | 2–3 pages |
| 3 | Devices & specifications (OS, CPU, GPU, RAM, storage, display, battery) | M2 (all provide data) | 1–2 pages |
| 4 | Experimental methodology | M1 | 1–2 pages |
| 5 | Results | M2 | 3–4 pages (mostly charts) |
| 6.1 | Performance comparison & best laptop (**Task 2**) | M2 | 1–2 pages |
| 6.2 | Comparison with public benchmarks (**Task 3**) | M3 | 2 pages |
| 6.3 | Cost & price/performance analysis (**Task 4**) | M4 | 2 pages |
| 7 | Additional experiments (throttling, battery vs plugged in, power modes, battery life) | M5 | 2 pages |
| 8 | Comparison across device types: laptop vs tablet vs phone | M5 | 1–2 pages |
| 9 | Recommendations & conclusion | M5 | 1 page |
| 10 | Member contributions (name, index no, what each did) | M2 | ½ page |
| — | References (IEEE style) · Appendix: raw data tables, screenshots, Geekbench links | M3 / all | — |

**Writing rules:** past tense, formal tone, every figure has a numbered caption and is mentioned in the text, every external number has a citation, units everywhere.

---

## 8. Presentation (12–15 min + 10 min Q&A)

| # | Part | Presenter | Time |
|---|---|---|---|
| 1 | Title, team, objectives, tools & what they measure, method | M1 | 2.5 min |
| 2 | Laptops & specs, results, best laptop | M2 | 3 min |
| 3 | Our results vs public benchmarks | M3 | 2.5 min |
| 4 | Cost, value, use-case recommendations | M4 | 2.5 min |
| 5 | Extra experiments, laptop vs tablet vs phone, conclusion | M5 | 2.5 min |
| — | Contribution slide → Q&A | All | — |

**Slide rules:** one message per slide (put it in the slide title, e.g. *"L3 wins short bursts, but L1 wins 30-minute renders"*), large charts, little text, the same laptop colours as the report. A throttling chart (clock speed dropping over time) is a strong visual. Bring the laptops if allowed.

---

## 9. Q&A preparation (everyone learns ALL of these)

1. What is the difference between single-core and multi-core scores? Which matters for which apps?
2. Why did laptop X beat laptop Y? (Answer with architecture: cores, clocks, cache, TDP, GPU, memory.)
3. Geekbench vs Cinebench: why can they rank laptops differently? (Short burst vs sustained; mixed workloads vs rendering.)
4. What is thermal throttling, and how did you measure it?
5. What are TDP, PL1 and PL2? Why does the same CPU perform differently in different laptops?
6. Why do your scores differ from the public results?
7. Synthetic vs real-world benchmarks: which are ours?
8. How is the Time Spy score calculated? What do the Graphics and CPU scores mean?
9. Why use a geometric mean for the overall score?
10. Why 3 runs? Why the median and not the mean?
11. How did you make the tests fair across laptops?
12. Integrated vs dedicated GPU: what's the difference? Why does dual-channel RAM matter for an iGPU?
13. What is a hybrid architecture (P-cores vs E-cores)?
14. Why does a laptop perform worse on battery?
15. What is performance per watt? Which laptop was most efficient?
16. Is it fair to compare a phone with a laptop? What are the limitations?
17. How did you choose the weights for each use case?
18. Which laptop has the best price/performance ratio, and why?
19. What is a bottleneck? Name one you found.
20. Amdahl's Law: why doesn't doubling the cores double the multi-core score?
21. What would you do differently / how would you improve the experiment?

**Mock Q&A:** in Week 3, each member asks the others 3 questions about **sections that aren't theirs**.

---

## 10. Timeline

> Dates assume the deadlines are 27 Oct (report) and 28 Oct (presentation). Adjust after M1 confirms.

| Dates | Milestone | Who |
|---|---|---|
| **Tue 7 – Thu 9 Oct** | Read this plan · fill in the device table · M1 confirms dates & tool versions · repo folders + templates ready · everyone pauses Windows Update | All / M1 |
| **Fri 10 – Mon 13 Oct** | **Everyone benchmarks their laptop** (Part 4) · spec sheets filled in · screenshots + CSV rows uploaded | All |
| **Tue 14 Oct** | M1's data quality check · **Checkpoint meeting #1** (30 min): review results | M1 / All |
| **Tue 14 – Sun 19 Oct** | M2 charts & ranking · M3 public data · M4 prices & value · M5 runs the extra experiments (owners run them on their own laptops) + phone/tablet tests · M1 writes Task 1 + methodology | Each lead |
| **Mon 20 Oct** | **All report sections drafted** · M4 shares the slide template · **Checkpoint meeting #2** | All |
| **Tue 21 – Thu 23 Oct** | M2 merges the report · everyone reviews one other section · slides built | M2 / M4 / All |
| **Fri 24 Oct** | **Rehearsal #1** (timed) + mock Q&A #1 | All |
| **Sat 25 Oct** | Report final proofread · slides fixed | M2 / M4 |
| **Sun 26 Oct** | **Rehearsal #2** + mock Q&A #2 · **submit report one day early** | All |
| Mon 27 Oct 11:59 pm | Official report deadline (we're already done) | — |
| Tue 28 Oct | Presentation & viva | All |

---

## 11. Checklist

- [ ] ≥3 laptops fully tested (3 runs × all tools) + phone + tablet for the comparison across types
- [ ] Every number has a screenshot or Geekbench link in `evidence/`
- [ ] Full spec table incl. OS, CPU, GPU, RAM (channel mode), storage, battery (Wh + health)
- [ ] Task 1: measures of performance explained for each benchmark
- [ ] Task 2: comparison + best overall laptop with justification
- [ ] Task 3: comparison with public benchmarks + references
- [ ] Task 4: prices with evidence + price/performance + use cases (gaming, content creation, student/office)
- [ ] Best price/performance device stated clearly
- [ ] Additional experiments: throttling, battery vs plugged in, power modes, battery life, comparison across device types
- [ ] Contribution table with **names + index numbers** (report AND slides)
- [ ] References in IEEE style
- [ ] Report submitted as PDF on Moodle · slides submitted
- [ ] Two full rehearsals done · every member can answer the questions in Part 9

---

## 12. Contributions (fill in at the end)

| Member | Name | Index No. | Role | Devices tested | Report sections | Slides |
|---|---|---|---|---|---|---|
| M1 | | | Benchmark Selection & Methodology | L1 | 1, 2, 4 | 1 |
| M2 | | | Results & Data Analysis, Report Editor | L2 | 3, 5, 6.1, 10 | 2 |
| M3 | | | Public Benchmark Comparison | L3 | 6.2, References | 3 |
| M4 | | | Cost & Value Analysis, Slides Lead | L4 | 6.3 | 4 |
| M5 | | | Additional Experiments & Comparison Across Device Types | L5 | 7, 8, 9 | 5 |
