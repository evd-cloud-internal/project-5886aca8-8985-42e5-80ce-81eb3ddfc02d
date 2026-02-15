---
name: Home
assetId: bf8a7964-1516-4176-8330-87098032ad88
type: page
---

# Sales Dashboard

{% dropdown
    id="category_filter"
    data="demo_daily_orders"
    value_column="category"
    title="Category"
    multiple=true
/%}

{% big_value
    data="demo_daily_orders"
    value="sum(total_sales)"
    fmt="usd1m"
    title="Total Sales"
    filters=["category_filter"]
    comparison={
        compare_vs="prior year"
    }
    sparkline={
        type="area"
        x="date"
        date_grain="month"
    }
/%}

{% big_value
    data="demo_daily_orders"
    value="sum(transactions)"
    title="Total Transactions"
    filters=["category_filter"]
    comparison={
        compare_vs="prior year"
    }
    sparkline={
        type="area"
        x="date"
        date_grain="month"
    }
/%}

{% big_value
    data="demo_daily_orders"
    value="avg(avg_transaction_value)"
    fmt="usd2"
    title="Avg Transaction Value"
    filters=["category_filter"]
    comparison={
        compare_vs="prior year"
    }
    sparkline={
        type="area"
        x="date"
        date_grain="month"
    }
/%}

## Sales Trend

{% line_chart
    data="demo_daily_orders"
    x="date"
    y="sum(total_sales)"
    y_fmt="usd0m"
    series="category"
    date_grain="month"
    filters=["category_filter"]
    title="Monthly Sales by Category"
/%}

## Category Breakdown

{% bar_chart
    data="demo_daily_orders"
    x="category"
    y="sum(total_sales)"
    y_fmt="usd0m"
    filters=["category_filter"]
    title="Total Sales by Category"
    order="sum(total_sales) desc"
/%}

## Yearly Performance

{% area_chart
    data="demo_daily_orders"
    x="date"
    y="sum(total_sales)"
    y_fmt="usd0m"
    series="category"
    date_grain="quarter"
    stacked=true
    filters=["category_filter"]
    title="Quarterly Sales (Stacked)"
/%}

## Summary Table

{% table
    data="demo_daily_orders"
    filters=["category_filter"]
    title="Sales by Category & Year"
    show_total_row=true
    show_total_column=true
%}
    {% dimension
        value="category"
    /%}
    {% pivot
        value="date"
        date_grain="year"
    /%}
    {% measure
        value="sum(total_sales)"
        fmt="usd0m"
        title="Sales"
    /%}
    {% measure
        value="sum(transactions)"
        fmt="#,##0"
        title="Transactions"
    /%}
{% /table %}
