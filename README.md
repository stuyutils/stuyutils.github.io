# Stuyutils

Currently only a cohort lookup app.

## To run locally

Clone the repository...

Install the dependencies...

```bash
cd stuyutils.github.io
npm install
```

...then start [Rollup](https://rollupjs.org):

```bash
npm run dev
```

Navigate to [localhost:5000](http://localhost:5000). You should see the app running. 

By default, the server will only respond to requests from localhost. To allow connections from other computers, edit the `sirv` commands in package.json to include the option `--host 0.0.0.0`.

## Cohorts

Look up stuy cohorts for 2020-2021. Data must be manually updated from the official spreadsheet.

### Updating data

In the src folder are data from certain dates. For example, data on 2020-09-14 is in file ```cohorts.20200914.ts```.

To update data:

- Create a new file, preferably with name ```cohorts.[date].ts```.
- In the file, default export the cohorts array, which is in the format of: [['OSIS1', 'Survey Choice1', 'Group'], ['OSIS2', 'Survey Choice2', 'Group2'], ...];
- Export current date with a Date object in a variable named ```date```.

- Inside src/Cohorts.svelte, import from your new file:
```javascript
import cohorts2021, {date} from "./[your_file_here]";
``` 

To run and see the changes locally,
```bash
npm run dev
```

To deploy the site with new data, first be sure to kill off the dev server (CTRL+C), then run,
```bash
npm run deploy
```
Make sure you have access to the original GitHub repo.
