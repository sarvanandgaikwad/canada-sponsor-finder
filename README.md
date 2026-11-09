# Canada Tech Sponsor Finder

Find Canadian companies that have hired foreign tech workers, using Government of Canada LMIA open data and Atlantic Immigration Program employer lists.

> 🚧 Work in progress — see the [project board](https://github.com/users/sarvanandgaikwad/projects/1/views/1).

## Tech stack
Python · FastAPI · PostgreSQL · React · TypeScript · Docker · AWS · GitHub Actions

## Project structure
| Folder | Purpose |
|---|---|
| `etl/` | Download, clean, and load data |
| `backend/` | FastAPI API |
| `frontend/` | React app |
| `infra/` | AWS infrastructure (Terraform) |
| `notebooks/` | Data exploration |
| `docs/` | Notes and decisions |

## Data sources
- Temporary Foreign Worker Program: Positive LMIA employers (open.canada.ca), Open Government Licence – Canada
- Atlantic Immigration Program designated employer lists (NS, NB, PEI, NL)

## Disclaimer
Historical LMIA approvals don't guarantee current hiring or sponsorship. Not immigration advice.