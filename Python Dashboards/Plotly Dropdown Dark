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
    "Revenue": np.random.normal(50000, 12000, n).astype(int),
    "Profit": np.random.normal(8000, 3000, n).astype(int),
    "Date": pd.date_range("2023-01-01", periods=n, freq="D")
})


dark_template = dict(
    layout=dict(
        paper_bgcolor='rgba(0,0,0,0)',
        plot_bgcolor='rgba(0,0,0,0)',
        font=dict(color='white'),  # Neutral text
        title=dict(font=dict(color='white', size=20)),
        xaxis=dict(color='white', gridcolor='rgba(255,255,255,0.1)'),
        yaxis=dict(color='white', gridcolor='rgba(255,255,255,0.1)'),
        legend=dict(font=dict(color='white')),
    )
)


fig_scatter = px.scatter(
    df, x="Revenue", y="Profit", color="Region", 
    title="Revenue vs Profit by Region", hover_data=["Product"]
)
fig_scatter.update_traces(marker=dict(line=dict(width=1, color='white'), size=10, opacity=0.8))
fig_scatter.update_layout(**dark_template['layout'])

fig_line = px.line(
    df, x="Date", y="Revenue", color="Region", 
    title="Revenue Over Time"
)
fig_line.update_traces(line=dict(width=3, shape='spline'))
fig_line.update_layout(**dark_template['layout'])

fig_hist = px.histogram(
    df, x="Revenue", nbins=30, color="Product", 
    title="Revenue Distribution by Product"
)
fig_hist.update_layout(**dark_template['layout'])

fig_box = px.box(
    df, x="Product", y="Profit", color="Product", 
    title="Profit Distribution per Product"
)
fig_box.update_layout(**dark_template['layout'])

figures = {
    "Scatter Plot": fig_scatter,
    "Line Chart": fig_line,
    "Histogram": fig_hist,
    "Box Plot": fig_box
}

app = dash.Dash(__name__)

app.layout = html.Div([
    html.H1(
        "📊 Sales Performance Dashboard", 
        style={
            "textAlign": "center", 
            "color": "white"  # Removed text shadow/glow
        }
    ),

    html.Div([
        html.Label("Select a plot:", style={"color": "white"}),
        dcc.Dropdown(
            id="plot-selector",
            options=[{"label": k, "value": k} for k in figures.keys()],
            value="Scatter Plot",
            clearable=False,
            style={
                "backgroundColor": "#1a1a2e", 
                "color": "white",
                "border": "1px solid white"
            }
        )
    ], style={"width": "30%", "margin": "auto", "paddingBottom": "20px"}),

    html.Div([
        dcc.Graph(id="main-graph")
    ])
], style={
    "background": "linear-gradient(to top right, #000000, #001f3f)", 
    "minHeight": "100vh", 
    "padding": "20px"
})

@app.callback(
    Output("main-graph", "figure"),
    Input("plot-selector", "value")
)
def update_graph(selected_plot):
    return figures[selected_plot]

if __name__ == "__main__":
    app.run(debug=True)
