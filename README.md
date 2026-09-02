# Predicting the NCAA Men's Gymnastics Team Champion

Can you tell who is going to win the national title before the national meet happens?

This project tries to predict the NCAA men's gymnastics team champion from regular-season data
alone. Every feature is computed from meets that finished on or before April 8, which falls between
the conference championships and the NCAA Championship, so nothing the model sees comes from the
event it is predicting.

Data is every NCAA team-season from 2013 through 2025, scraped from the
[Road to Nationals](https://www.roadtonationals.com) API. 2020 is missing because the season was
cancelled. That comes out to 185 team-seasons with 12 champions between them. The 2026 season was
then used as an actual forward test, predicted before the meet was held.

The written report is [416_Final_Report.pdf](https://github.com/angrapsas/NCAA-Champion-Prediction-Model/raw/main/416_Final_Report.pdf).

## Results

- Picking the team with the best average score only gets 7 of 12 seasons right.
- A single number, a team's NQA (National Qualifying Average) on **parallel bars**, identifies the
  champion in all 12 labeled seasons, and in 2026 as well. Thirteen for thirteen, with no model.
- A logistic regression on 27 features called 2024 and 2025 correctly. On 2026 it picked out all
  four eventual top-four finishers but ranked Oklahoma first and Stanford second, and Stanford won
  by 1.33 points.

The interesting result is not the classifier. It is that one well-chosen feature beat everything
built on top of it, and that we only found that feature by reading the model's weights.

## Running it

The notebook runs top to bottom. On a cold run it makes roughly 1,700 requests to the Road to
Nationals API, most of them in the data-integrity section, so expect it to take a while. It caches
what it fetches, so a second run is fast.

```bash
pip install -r requirements.txt
jupyter notebook NCAA_Champion_Model.ipynb
```

It also runs in Google Colab, where the first cell mounts Drive to cache the fetched data.

## Files

| | |
|---|---|
| `NCAA_Champion_Model.ipynb` | The project, with outputs |
| [`416_Final_Report.pdf`](https://github.com/angrapsas/NCAA-Champion-Prediction-Model/raw/main/416_Final_Report.pdf) | The written report, submitted for CSCI 416 at William & Mary |
| `requirements.txt` | Packages needed to run it |

## A note on the numbers

Road to Nationals is a live database and its historical records get corrected over time. The counts
in the data-integrity section come from a run in spring 2026, and a later run will produce slightly
different ones. The conclusions have been stable.
