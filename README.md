# functions
1. orderedSince reusable function
```ts
const sec = 1000;
const min = 60 * sec; // 60000
const hr = 60 * min; // 600000
const day = 24 * hr;
const wk = 7 * day;
const mth = 30 * day;
const yr = 365 * day;

const time_diff = (time_string: string) => {
	return new Date().getTime() - new Date(time_string).getTime();
};

const orderedSince = (created_at: string) => {
	const time = time_diff(created_at);
	let x = 0;
  let y = 0;
	let type;
  let type2;

	if (time < min) {
		// if time is less than a minute
		return 'less than a minute ago';
	} else if (time > min && time < hr) {
		// if time is greater than a minute but less than an hour
		x = Math.floor(time / min);
    y = Math.floor(time/sec) - (x*60)
		type = 'minute';
    type2 = 'seconds';
	} else if (time > hr && time < day) {
		// if time is greater than an hour but less than a day
		x = Math.floor(time / hr);
		y = Math.floor(time/min) - (x*60);
		type = 'hour';
    type2 = 'minutes'
	} else if (time > day && time < wk) {
		// if time is greater than a day but less than a week
		x = Math.floor(time / day);
    y = Math.floor(time/hr) - (x*24)
		type = 'day';
    type2 = 'hours'
	} else if (time > wk && time < mth) {
		// if time is greater than a week but less than a month
		x = Math.floor(time / wk);
    y = Math.floor(time/day) - (x*7)
		type = 'week';
    type2 = 'days'
	} else if (time > mth && time < yr) {
		// if time is greater than a month but less than a year
		x = Math.floor(time / mth);
    y = Math.floor(time/day) - (x*30)
    console.log(y)
		type = 'month';
    type2 = 'days'
	} else if (time > yr) {
		// if time is greater than a year
		x = Math.floor(time / yr);
    y = Math.floor(time/mth) - (x*12)
		type = 'year';
    type2 = 'month'
	}

  return `${x>1 ? `${x} ${type}s`: `${x} ${type}`} ${y>0 ? `${y} ${type2}`: '' } ago`.trim()
};

const a = orderedSince('Fri Jun 17 2022 24:00:00 GMT+0600 (Bangladesh Standard Time)')
console.log(a) 
```