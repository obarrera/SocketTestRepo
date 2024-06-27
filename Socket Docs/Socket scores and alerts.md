Socket scores and alerts are broken down into the following categories:

- Supply chain risk
- Quality
- Maintenance
- Vulnerabilities
- License

We compute the score for each category as a normalized weighted sum of various metrics.  These metrics are subject to change as we make improvements to our product.  Each metric may also optionally apply a limit.  Given a category $$i$$, let $$x_{i,j}$$ be the value of metric $$j$$ with normalization function $$N_j$$ and weight $$w_j$$ and limit $$l_{i,j}$$.  Then the score $$S_i$$ is

$$S_i = 100 \\cdot \\min \\left ( \\max \\left ( 0, \\min_{j} l_{i,j} \\right ), \\frac{\\sum_{j} w\_{j} N_j(x_j)}{ \\sum_j w_j} \\right )^{\\gamma}$$

Where $$\\gamma$$ is a power scaling constant based on the size and popularity of the project:

$$\\gamma \\approx \\frac{1}{\\frac{1}{2} + c_0 \\log(\\textrm{lines of code}) + c_1 \\log(\\textrm{popularity})}$$

Currently socket supports the following metrics:

| Metric                         | Category          | Weight | Normalization                    | Limit                                                                                     |
| ------------------------------ | ----------------- | ------ | -------------------------------- | ----------------------------------------------------------------------------------------- |
| Critical Alerts                | Any               | 1      | $$e^{-10 x}$$                    | $$\\begin{cases} \\frac{1}{4} & \\text{if } x > 0 \\ 1 & \\text{otherwise} \\end{cases}$$ |
| High Alerts                    | Any               | 2      | $$e^{-x}$$                       | $$\\max \\left ( \\frac{1}{4}, 1 - \\frac{x}{10} \\right )$$                              |
| Medium Alerts                  | Any               | 2      | $$e^{-\\frac{x}{20}}$$           | $$\\max \\left ( \\frac{1}{2}, 1.15 - \\frac{x}{20} \\right )$$                           |
| Low Alerts                     | Any               | 3      | $$e^{-\\frac{x}{40}}$$           | $$1$$                                                                                     |
| License Quality                | License           | 12     | $$\\frac{x}{100}$$               | $$\\begin{cases} 0 & \\text{if } x = 0 \\ 1 & \\text{otherwise} \\end{cases}$$            |
| Maintainer Count               | Maintenance       | 5      | $$-(e^{-\\frac{x}{3}} - 1)$$     | $$1$$                                                                                     |
| Versions Last Year             | Maintenance       | 5      | $$-(e^{-\\frac{x}{12}} - 1)$$    | $$1$$                                                                                     |
| Versions Last Two Months       | Maintenance       | 3      | $$-(e^{-\\frac{x}{2}} - 1)$$     | $$1$$                                                                                     |
| Versions Last Month            | Maintenance       | 2      | $$-(e^{-x} - 1)$$                | $$1$$                                                                                     |
| Versions Last Week             | Maintenance       | 1      | $$-(e^{-\\frac{x}{0.25}} - 1)$$  | $$1$$                                                                                     |
| Open Issues                    | Maintenance       | 1      | $$e^{-\\frac{x}{100}}$$          | $$1$$                                                                                     |
| Closed Issues                  | Maintenance       | 1      | $$-(e^{-\\frac{x}{1000}} - 1)$$  | $$1$$                                                                                     |
| Commits Last Week              | Maintenance       | 1      | $$-(e^{-\\frac{x}{4}} - 1)$$     | $$1$$                                                                                     |
| Commits Last Month             | Maintenance       | 1      | $$-(e^{-\\frac{x}{16}} - 1)$$    | $$1$$                                                                                     |
| Commits Last Two Months        | Maintenance       | 1      | $$-(e^{-\\frac{x}{32}} - 1)$$    | $$1$$                                                                                     |
| Commits Last Year              | Maintenance       | 1      | $$-(e^{-\\frac{x}{208}} - 1)$$   | $$1$$                                                                                     |
| Commits                        | Maintenance       | 1      | $$-(e^{-\\frac{x}{300}} - 1)$$   | $$1$$                                                                                     |
| Version Count                  | Maintenance       | 0.5    | $$-(e^{-\\frac{x}{10}} - 1)$$    | $$1$$                                                                                     |
| Readme Length                  | Quality           | 5      | $$\\frac{x}{100}$$               | $$1$$                                                                                     |
| Bundle Size                    | Quality           | 2      | $$e^{-\\frac{x}{16384}}$$        | $$1$$                                                                                     |
| Stargazers                     | Quality           | 1      | $$-(e^{-\\frac{x}{100}} - 1)$$   | $$1$$                                                                                     |
| Forks                          | Quality           | 1      | $$-(e^{-x} - 1)$$                | $$1$$                                                                                     |
| Watchers                       | Quality           | 1      | $$-(e^{-x} - 1)$$                | $$1$$                                                                                     |
| Lines of Code                  | Quality           | 0.5    | $$\\frac{x}{50}$$                | $$1$$                                                                                     |
| Download Count                 | Supply Chain Risk | 5      | $$-(e^{-\\frac{x}{10000}} - 1)$$ | $$1$$                                                                                     |
| Transitive Dependency Count    | Supply Chain Risk | 1      | $$e^{-\\frac{x}{1000}}$$         | $$1$$                                                                                     |
| Total Dependency Count         | Supply Chain Risk | 1      | $$e^{-\\frac{x}{1000}}$$         | $$1$$                                                                                     |
| Dependency Count               | Supply Chain Risk | 1      | $$e^{-\\frac{x}{50}}$$           | $$1$$                                                                                     |
| Dev Dependency Count           | Supply Chain Risk | 0.5    | $$e^{-\\frac{x}{100}}$$          | $$1$$                                                                                     |
| Dependency Vulnerability Count | Vulnerability     | 1      | $$1 - x$$                        | $$\\begin{cases} 0.5 & \\text{if } x > 0 \\ 1 & \\text{otherwise} \\end{cases}$$          |
| Vulnerability Count            | Vulnerability     | 1      | $$1 - \\frac{x}{3}$$             | $$1$$                                                                                     |

Please note that these metrics are subject to change and may be revised as we make changes to our system.  The contents of this document may not exactly represent the scoring system as deployed in Socket at this point in time as we are continuously making adjustments to these systems.
