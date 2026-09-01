# Live Export

A snapshot of the categories and questions currently published on the live
Open-Trivia instance. Exported 2026-09-01T19:25:03Z.

**44 categories, 53394 questions.** Only enabled categories and enabled questions
are included; disabled rows and internal test categories are left out.

This directory is generated. Edit questions in the app and re-run the export
rather than patching these files by hand. The hand-curated packs under
`../categories/` (the Uberspot conversion) are separate and are not touched by
this export.

## Layout

| Path | Contents |
| --- | --- |
| `questions.csv` | Every exported question in one file. |
| `split_by_category/<slug>.csv` | One file per category, same columns. |
| `category_archives/<slug>.zip` | Importable pack: `questions.csv` at the zip root. |
| `manifest.json` | Export timestamp plus per-category counts and file paths. |

## CSV Format

Columns match the app's import template:

```
category_name,question_text,option_a,option_b,option_c,option_d,correct_answer,complexity,disabled,image_url
```

- `correct_answer` is `A`, `B`, `C` or `D`.
- `complexity` is `easy`, `medium` or `hard`.
- `disabled` is always `false` here, since disabled questions are excluded.
- `image_url` is blank for most questions. 378 questions carry one, and all of
  those point at external URLs rather than files stored in this repo, so the
  packs contain no `images/` folder.

`Apple Certification` exists on the live instance but has no questions yet, so
its CSV is a header row only and its zip holds that header row.

## Regenerating

Run against the live Postgres database:

```sql
\copy (
  SELECT c.name AS category_name, q.text AS question_text,
         q.option_a, q.option_b, q.option_c, q.option_d,
         q.correct_answer, q.complexity,
         CASE WHEN COALESCE(q.disabled, false) THEN 'true' ELSE 'false' END AS disabled,
         NULLIF(q.image_url, '') AS image_url
  FROM questions q
  JOIN categories c ON c.id = q.category_id
  WHERE COALESCE(c.disabled, false) = false
    AND COALESCE(q.disabled, false) = false
  ORDER BY c.name, q.id
) TO STDOUT WITH (FORMAT csv, HEADER true)
```

Then split the result by `category_name` into `split_by_category/`, zip each
one as `questions.csv`, and rewrite `manifest.json`. Slugs are the category
name lowercased with every run of non-alphanumeric characters collapsed to a
single hyphen.

## Categories

| Category | Slug | Questions | With image | Files |
| --- | --- | --- | --- | --- |
| Animals | `animals` | 1366 | 0 | [csv](split_by_category/animals.csv) / [zip](category_archives/animals.zip) |
| Apple Certification | `apple-certification` | 0 | 0 | [csv](split_by_category/apple-certification.csv) / [zip](category_archives/apple-certification.zip) |
| Brain Teasers | `brain-teasers` | 207 | 0 | [csv](split_by_category/brain-teasers.csv) / [zip](category_archives/brain-teasers.zip) |
| Celebrities | `celebrities` | 3196 | 0 | [csv](split_by_category/celebrities.csv) / [zip](category_archives/celebrities.zip) |
| Computer - AWS Solutions Architect Certificate | `computer-aws-solutions-architect-certificate` | 461 | 0 | [csv](split_by_category/computer-aws-solutions-architect-certificate.csv) / [zip](category_archives/computer-aws-solutions-architect-certificate.zip) |
| Computer - ArgoCD | `computer-argocd` | 100 | 9 | [csv](split_by_category/computer-argocd.csv) / [zip](category_archives/computer-argocd.zip) |
| Computer - ArgoCD v2 | `computer-argocd-v2` | 100 | 9 | [csv](split_by_category/computer-argocd-v2.csv) / [zip](category_archives/computer-argocd-v2.zip) |
| Computer - CompTIA Netwroking+ | `computer-comptia-netwroking` | 470 | 0 | [csv](split_by_category/computer-comptia-netwroking.csv) / [zip](category_archives/computer-comptia-netwroking.zip) |
| Computer - Comptia A+ | `computer-comptia-a` | 43 | 0 | [csv](split_by_category/computer-comptia-a.csv) / [zip](category_archives/computer-comptia-a.zip) |
| Computer - DevOps | `computer-devops` | 100 | 6 | [csv](split_by_category/computer-devops.csv) / [zip](category_archives/computer-devops.zip) |
| Computer - DevOps v2 | `computer-devops-v2` | 100 | 6 | [csv](split_by_category/computer-devops-v2.csv) / [zip](category_archives/computer-devops-v2.zip) |
| Computer - Git Source Control | `computer-git-source-control` | 250 | 0 | [csv](split_by_category/computer-git-source-control.csv) / [zip](category_archives/computer-git-source-control.zip) |
| Computer - GitLab | `computer-gitlab` | 100 | 0 | [csv](split_by_category/computer-gitlab.csv) / [zip](category_archives/computer-gitlab.zip) |
| Computer - Kong | `computer-kong` | 100 | 9 | [csv](split_by_category/computer-kong.csv) / [zip](category_archives/computer-kong.zip) |
| Computer - Kong v2 | `computer-kong-v2` | 100 | 9 | [csv](split_by_category/computer-kong-v2.csv) / [zip](category_archives/computer-kong-v2.zip) |
| Computer - Kubernetes | `computer-kubernetes` | 100 | 8 | [csv](split_by_category/computer-kubernetes.csv) / [zip](category_archives/computer-kubernetes.zip) |
| Computer - Kubernetes v2 | `computer-kubernetes-v2` | 100 | 8 | [csv](split_by_category/computer-kubernetes-v2.csv) / [zip](category_archives/computer-kubernetes-v2.zip) |
| Computer - Traefik | `computer-traefik` | 100 | 7 | [csv](split_by_category/computer-traefik.csv) / [zip](category_archives/computer-traefik.zip) |
| Computer - Traefik v2 | `computer-traefik-v2` | 100 | 7 | [csv](split_by_category/computer-traefik-v2.csv) / [zip](category_archives/computer-traefik-v2.zip) |
| Entertainment | `entertainment` | 280 | 0 | [csv](split_by_category/entertainment.csv) / [zip](category_archives/entertainment.zip) |
| For Kids | `for-kids` | 759 | 0 | [csv](split_by_category/for-kids.csv) / [zip](category_archives/for-kids.zip) |
| General | `general` | 3292 | 0 | [csv](split_by_category/general.csv) / [zip](category_archives/general.zip) |
| Geography | `geography` | 842 | 0 | [csv](split_by_category/geography.csv) / [zip](category_archives/geography.zip) |
| Geology General | `geology-general` | 50 | 0 | [csv](split_by_category/geology-general.csv) / [zip](category_archives/geology-general.zip) |
| Geology Identification - Rocks | `geology-identification-rocks` | 20 | 20 | [csv](split_by_category/geology-identification-rocks.csv) / [zip](category_archives/geology-identification-rocks.zip) |
| Geology Identification - Stones & Gems | `geology-identification-stones-gems` | 70 | 70 | [csv](split_by_category/geology-identification-stones-gems.csv) / [zip](category_archives/geology-identification-stones-gems.zip) |
| Geology Mohs Hardness | `geology-mohs-hardness` | 210 | 210 | [csv](split_by_category/geology-mohs-hardness.csv) / [zip](category_archives/geology-mohs-hardness.zip) |
| History | `history` | 1645 | 0 | [csv](split_by_category/history.csv) / [zip](category_archives/history.zip) |
| Hobbies | `hobbies` | 1242 | 0 | [csv](split_by_category/hobbies.csv) / [zip](category_archives/hobbies.zip) |
| Humanities | `humanities` | 1097 | 0 | [csv](split_by_category/humanities.csv) / [zip](category_archives/humanities.zip) |
| Literature | `literature` | 1288 | 0 | [csv](split_by_category/literature.csv) / [zip](category_archives/literature.zip) |
| Movies | `movies` | 4313 | 0 | [csv](split_by_category/movies.csv) / [zip](category_archives/movies.zip) |
| Music | `music` | 5579 | 0 | [csv](split_by_category/music.csv) / [zip](category_archives/music.zip) |
| Newest | `newest` | 3016 | 0 | [csv](split_by_category/newest.csv) / [zip](category_archives/newest.zip) |
| People | `people` | 2743 | 0 | [csv](split_by_category/people.csv) / [zip](category_archives/people.zip) |
| Python | `python` | 1000 | 0 | [csv](split_by_category/python.csv) / [zip](category_archives/python.zip) |
| Rated | `rated` | 2185 | 0 | [csv](split_by_category/rated.csv) / [zip](category_archives/rated.zip) |
| Religion Faith | `religion-faith` | 638 | 0 | [csv](split_by_category/religion-faith.csv) / [zip](category_archives/religion-faith.zip) |
| Science | `science` | 2 | 0 | [csv](split_by_category/science.csv) / [zip](category_archives/science.zip) |
| Science Technology | `science-technology` | 2486 | 0 | [csv](split_by_category/science-technology.csv) / [zip](category_archives/science-technology.zip) |
| Sports | `sports` | 2840 | 0 | [csv](split_by_category/sports.csv) / [zip](category_archives/sports.zip) |
| Television | `television` | 5230 | 0 | [csv](split_by_category/television.csv) / [zip](category_archives/television.zip) |
| Video Games | `video-games` | 599 | 0 | [csv](split_by_category/video-games.csv) / [zip](category_archives/video-games.zip) |
| World | `world` | 4875 | 0 | [csv](split_by_category/world.csv) / [zip](category_archives/world.zip) |
