# Tuition Payback Plotter

**AppADay Day 161** | Category D, Data Viz | Claude API: No

Live: https://augustineiacopelli.github.io/appaday-161-tuition-payback-plotter/
Portfolio: https://augustineiacopelli.github.io/appaday/

Tuition Payback Plotter answers one question: how long until a degree, certificate, or bootcamp pays for itself through the raise it brings? Enter what the program costs and what it should do for your salary, and the app shows the break even point in years and months, a set of supporting numbers, and a chart of your extra earnings climbing toward the total cost.

## Inputs

Program cost can be entered two ways, chosen with the toggle at the top of the inputs card.

Itemized, the default, starts with program length: total credit hours, number of classes, and number of semesters. Fill in only the ones your costs use. Below that is a list of cost lines, and each line has a name, an amount, and how it is charged: per credit hour, per class, per semester, or one time. The list starts with Tuition per credit hour, Fees per semester, and Books and supplies per class. Add a cost puts in a new line (up to 12), and the x button removes one. Under each line the app shows the math, such as $450 x 36 credit hours = $16,200. If a line is charged per credit hour, class, or semester and that count is still blank, the line and an inline message point to the missing number.

The Living on campus switch adds room and board. Enter housing and the meal plan per semester, and optionally the rent and food you would pay anyway per semester, so only the extra cost counts. Room and board is (housing + meal plan minus current living costs) times the number of semesters, and it never goes below zero. A Program cost bar at the bottom of the builder shows the running total, split into tuition and fees and room and board.

One total skips the builder and takes a single program cost figure, for when you already know the number.

Current annual income is what you earn now, and expected salary after is what you expect to earn once you finish. Both are required.

Opportunity cost is optional and defaults to 0. It is pay you give up while studying, such as cutting back to part time, and it is added to the program cost to make the total investment. Annual raise is also optional, defaults to 0, and accepts 0 to 25 percent.

Money fields accept plain numbers, commas, a leading dollar sign, or shorthand like 45k. Fields reformat with commas when you leave them. Results recalculate as you type, after a short pause, and any field with a problem shows its message directly beneath it. Try an example, under the introduction, fills in a sample itemized program.

The time horizon toggle sets the chart and the net figure to 5, 10, or 20 years. It defaults to 10.

## The formula

The salary bump is expected salary minus current income. The total cost is program cost plus opportunity cost. Each year, the bump is added to a running total of extra earnings, and with an annual raise of r percent the bump in year t is bump times (1 + r) to the power of (t minus 1), so the gap between the two salaries grows each year.

Payback is the first moment the running total reaches the total cost. Within the crossover year the app interpolates linearly, so a $10,000 program with an $8,000 bump pays back in 1.25 years, shown as 1 yr 3 mo. Years and months are shown by flooring the years and rounding the months, and 12 months rolls into the next year.

The payback is always reported as the true value up to 100 years, even past the chosen horizon. When it falls past the horizon the result says so and suggests a longer view. The supporting cards show the total cost with its parts (program, room and board, and lost pay), the year one bump and whether it grows, the net gain or loss at the end of the horizon with the return on cost, and the conservative payback.

## The conservative scenario

Raises do not always arrive as hoped. The dashed line on the chart and the Conservative card repeat the calculation using only part of the expected bump. The gear in the header opens Settings, where you can set that share to 50, 75, or 90 percent. It defaults to 75 percent.

## The chart

The chart uses a linear year axis. A solid gold line with a light fill shows cumulative extra earnings, a dashed line shows the conservative scenario, a flat coral line shows the total cost, and a white dot labeled Break even marks the crossover when it falls within the horizon. Hover or tap the chart for exact values at any year.

## Edge cases

If the expected salary is equal to or lower than current income, there is no raise to recover the cost, so the result reads Never, on salary alone and the earnings lines stay flat at zero. A program with no cost pays back right away. If the payback would take longer than 100 years, the result says it does not pay back within a working lifetime.

## Saving

Your inputs, cost lines, cost mode, horizon, and conservative setting are saved on this device only under the localStorage key appaday-161-payback. Settings has a Clear saved inputs button that asks for a second tap before it clears everything back to the defaults, including the three starter cost lines.

## Tests

On load the app runs seven checks and logs the result to the console: $10,000 cost with an $8,000 bump returns 1.25 years shown as 1 yr 3 mo; the same with a 10 percent raise returns about 1.227 years; $100,000 cost with a $5,000 bump over 10 years is not achieved with a true payback of 20 years; a zero or negative bump returns null; an itemized program of $450 x 36 credit hours, $600 x 4 semesters, $120 x 12 classes, and a $250 one time cost totals $20,290, with $20,000 of room and board at $3,800 housing and $2,200 meals less $1,000 per semester over 4 semesters; and a living cost offset larger than room and board counts as zero rather than a credit.

## Built with

One self contained index.html with inline CSS and JavaScript, the Manrope font from Google Fonts, and Chart.js 4 from jsdelivr. It can be saved to a phone home screen with its own icon and opens full screen.

This calculator compares salaries only. It does not account for taxes, loan interest, or the value of a program beyond pay, so treat the result as one input to the decision rather than the answer.
