import dash
from dash import dcc, html, Input, Output
import plotly.express as px
import pandas as pd
import numpy as np


np.random.seed(42)
n = 200
df = pd.DataFrame({
    "Region": np.random.choice(["North", "South", "East", "West"], n),
    "Product": np.random.choice(["Laptop", "Phone", "Tablet", "Monitor"], n),
    "Revenue": np.random.normal(50000, 12000, n).astype(int),   # average 50k
    "Profit": np.random.normal(8000, 3000, n).astype(int),      # average 8k
    "Date": pd.date_range("2023-01-01", periods=n, freq="D")
})


fig_scatter = px.scatter(
    df, x="Revenue", y="Profit", color="Region", 
    title="Revenue vs Profit by Region", hover_data=["Product"]
)

fig_line = px.line(
    df, x="Date", y="Revenue", color="Region", 
    title="Revenue Over Time"
)

fig_hist = px.histogram(
    df, x="Revenue", nbins=30, color="Product", 
    title="Revenue Distribution by Product"
)

fig_box = px.box(
    df, x="Product", y="Profit", color="Product", 
    title="Profit Distribution per Product"
)

figures = {
    "Scatter Plot": fig_scatter,
    "Line Chart": fig_line,
    "Histogram": fig_hist,
    "Box Plot": fig_box
}


app = dash.Dash(__name__)

app.layout = html.Div([
    html.H1("📊 Sales Performance Dashboard", style={"textAlign": "center"}),

    html.Div([
        html.Label("Select a plot:"),
        dcc.Dropdown(
            id="plot-selector",
            options=[{"label": k, "value": k} for k in figures.keys()],
            value="Scatter Plot",
            clearable=False
        )
    ], style={"width": "30%", "margin": "auto"}),

    html.Div([
        dcc.Graph(id="main-graph")
    ])
])


@app.callback(
    Output("main-graph", "figure"),
    Input("plot-selector", "value")
)
def update_graph(selected_plot):
    return figures[selected_plot]

if __name__ == "__main__":
    app.run(debug=True)
