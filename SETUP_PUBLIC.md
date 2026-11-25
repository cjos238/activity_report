# Quick Reference - Two Repository Structure

## Public Repository: `activity_report/`

This is what appears on GitHub:
- `README.md` - Your public activity dashboard
- `.gitignore` - Excludes the private tool

**What to do:**
1. Push this to GitHub public
2. It shows only the generated README with activity metrics
3. No tool code is exposed

```bash
cd activity_report/
git push origin main
```

---

## Private Repository: `activity_report/activity_reporter/`

This is your local private tool:
- Source code (src/)
- Configuration (config.yaml)
- Documentation
- All tool files

**What to do:**
1. Keep this as a separate local git repo
2. Never push to public GitHub
3. Run `python dashboard.py` to generate the report
4. Report goes to `../README.md` (public repo)

```bash
cd activity_report/activity_reporter/
python dashboard.py
```

---

## Workflow

**Step 1: Generate Report (Private)**
```bash
cd activity_report/activity_reporter/
python dashboard.py
```
✓ Generates `../README.md` with activity metrics

**Step 2: Publish Report (Public)**
```bash
cd activity_report/
git add README.md
git commit -m "chore: update activity dashboard"
git push origin main
```
✓ Pushes README to public GitHub

---

## Directory Tree

```
activity_report/                    (PUBLIC git repo)
├── .git/                           (Public repo commits)
├── .gitignore                      (Hides activity_reporter)
├── README.md                       (Generated report)
│
└── activity_reporter/              (PRIVATE git repo)
    ├── .git/                       (Private repo commits)
    ├── src/
    │   ├── models.py
    │   ├── config_loader.py
    │   ├── git_metrics.py
    │   ├── readme_generator.py
    │   └── dashboard.py
    ├── config.yaml                 (Edit with your projects)
    ├── dashboard.py                (Entry point)
    ├── requirements.txt
    └── [documentation]
```

---

## Configuration

Edit `activity_report/activity_reporter/config.yaml`:

```yaml
projects:
  - ~/projects/ProjectA
  - ~/projects/ProjectB

readme_output_path: ../README.md
```

**Key point:** `../README.md` writes to parent directory (activity_report/)

---

## Automation

### Linux/macOS (Cron)

```bash
0 9 * * * cd /path/to/activity_report/activity_reporter && python dashboard.py && cd .. && git add README.md && git commit -m "chore: update dashboard" && git push
```

### Windows (Task Scheduler)

1. Run: `python /path/to/activity_reporter/dashboard.py`
2. Working dir: `/path/to/activity_reporter`
3. After completion: Manually commit and push from `activity_report/`

---

## Git Setup

### Initialize Private Repository

```bash
cd activity_report/activity_reporter/
git init
git add .
git commit -m "Initial commit: activity reporter tool"
# Keep local - don't push
```

### Initialize Public Repository

```bash
cd activity_report/
git init
git remote add origin https://github.com/yourusername/activity-report.git
git add README.md .gitignore
git commit -m "Initial commit: activity dashboard"
git push -u origin main
```

---

## Privacy Checklist

✅ `activity_reporter/` in `.gitignore` of public repo  
✅ No tool code in public repo  
✅ Only `README.md` and `.gitignore` in public repo  
✅ `activity_reporter/` has its own private git  
✅ Public README shows only metrics, no details  
✅ Automated generation protects privacy  

---

## Troubleshooting

**Q: Where do I edit the configuration?**
A: `activity_report/activity_reporter/config.yaml`

**Q: Where does the report get written?**
A: `activity_report/README.md` (parent directory)

**Q: How do I run the tool?**
A: `cd activity_report/activity_reporter/` then `python dashboard.py`

**Q: Can I push activity_reporter to GitHub?**
A: No - it's excluded by `.gitignore` and kept private

**Q: What if the .gitignore isn't working?**
A: Ensure `activity_reporter/` is on a separate `.git` (private repo)

---

**Setup Complete!** 🎉

Your public activity dashboard is ready to deploy on GitHub!
