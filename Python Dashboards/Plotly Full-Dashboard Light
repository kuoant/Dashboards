import dash
from dash import dcc, html
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


app = dash.Dash(__name__)


fig_scatter = px.scatter(
    df, x="Revenue", y="Profit", color="Region",
    title="Revenue vs Profit by Region", hover_data=["Product"],
    template="plotly_white", color_discrete_sequence=px.colors.qualitative.Pastel
)

fig_line = px.line(
    df, x="Date", y="Revenue", color="Region",
    title="Revenue Over Time", template="plotly_white",
    color_discrete_sequence=px.colors.qualitative.Vivid
)

fig_hist = px.histogram(
    df, x="Revenue", nbins=30, color="Product",
    title="Revenue Distribution by Product", template="plotly_white",
    color_discrete_sequence=px.colors.qualitative.Safe
)

fig_box = px.box(
    df, x="Product", y="Profit", color="Product",
    title="Profit Distribution per Product", template="plotly_white",
    color_discrete_sequence=px.colors.qualitative.Bold
)


card_style = {
    "backgroundColor": "#f9f9f9",  # light card background
    "borderRadius": "12px",
    "padding": "15px",
    "margin": "10px",
    "flex": "1",
    "boxShadow": "0px 4px 15px rgba(0,0,0,0.1)"
}


app.layout = html.Div(
    style={
        "backgroundColor": "#f0f2f5",  # page background
        "fontFamily": "Arial, sans-serif",
        "color": "#333",
        "padding": "20px"
    },
    children=[
        html.H1("📊 Sales Performance Dashboard",
                style={"textAlign": "center", "marginBottom": "30px", "color": "#3b82f6"}),

        html.Div([
            html.Div(dcc.Graph(figure=fig_scatter), style=card_style),
            html.Div(dcc.Graph(figure=fig_line), style=card_style),
        ], style={"display": "flex", "flexWrap": "wrap"}),

        html.Div([
            html.Div(dcc.Graph(figure=fig_hist), style=card_style),
            html.Div(dcc.Graph(figure=fig_box), style=card_style),
        ], style={"display": "flex", "flexWrap": "wrap"}),
    ]
)

if __name__ == "__main__":
    app.run(debug=True)
