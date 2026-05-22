
<div className="min-h-screen bg-gradient-to-br from-slate-900 via-slate-800 to-slate-900">
{/* Header */}
<div className="bg-slate-900 border-b border-slate-700 sticky top-0 z-40 shadow-lg">
<div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4">
<button
onClick={() => setSelectedStock(null)}
className=“text-cyan-400 hover:text-cyan-300 font-semibold mb-3 transition-colors”
>
← Back to Stocks
</button>
<div className="flex justify-between items-start">
<div>
<h1 className="text-4xl font-bold text-white mb-1">{stock.name}</h1>
<p className="text-slate-400">{stock.sector} • {stock.industry}</p>
</div>
<div className="text-right">
<p className="text-3xl font-bold text-white">₹{stock.price}</p>
<p className={`text-lg font-semibold ${stock.priceChange >= 0 ? 'text-green-400' : 'text-red-400'}`}>
{stock.priceChange >= 0 ? ‘+’ : ‘’}{stock.priceChange}%
</p>
</div>
</div>
</div>
</div>

```
    {/* Tab Navigation */}
    <div className="bg-slate-800 border-b border-slate-700">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="flex space-x-1 overflow-x-auto">
          {['overview', 'financials', 'institutional', 'news', 'concall', 'swot', 'rating'].map(tab => (
            <button
              key={tab}
              onClick={() => setActiveTab(tab)}
              className={`px-4 py-3 font-semibold whitespace-nowrap border-b-2 transition-colors ${
                activeTab === tab
                  ? 'border-cyan-400 text-cyan-400'
                  : 'border-transparent text-slate-400 hover:text-slate-300'
              }`}
            >
              {tab.charAt(0).toUpperCase() + tab.slice(1)}
            </button>
          ))}
        </div>
      </div>
    </div>

    {/* Content */}
    <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
      {/* Overview Tab */}
      {activeTab === 'overview' && (
        <div className="space-y-6">
          <div className="bg-slate-800 rounded-lg p-6 border border-slate-700">
            <h2 className="text-2xl font-bold text-white mb-4">Company Overview</h2>
            <p className="text-slate-300 text-lg leading-relaxed">{stock.description}</p>
            <div className="grid grid-cols-2 md:grid-cols-4 gap-4 mt-6">
              <div className="bg-slate-700 rounded p-4">
                <p className="text-slate-400 text-sm">Market Cap</p>
                <p className="text-white font-bold text-lg">{stock.marketCap}</p>
              </div>
              <div className="bg-slate-700 rounded p-4">
                <p className="text-slate-400 text-sm">NSE Ticker</p>
                <p className="text-white font-bold text-lg">{stock.nseSymbol}</p>
              </div>
              <div className="bg-slate-700 rounded p-4">
                <p className="text-slate-400 text-sm">P/E Ratio</p>
                <p className="text-green-400 font-bold text-lg">{stock.pe} ✓</p>
              </div>
              <div className="bg-slate-700 rounded p-4">
                <p className="text-slate-400 text-sm">D/E Ratio</p>
                <p className="text-green-400 font-bold text-lg">{stock.de} ✓</p>
              </div>
            </div>
          </div>
        </div>
      )}

      {/* Financials Tab */}
      {activeTab === 'financials' && (
        <div className="space-y-6">
          <div className="bg-slate-800 rounded-lg p-6 border border-slate-700">
            <h2 className="text-2xl font-bold text-white mb-4">Financial Metrics</h2>
            <div className="grid grid-cols-2 md:grid-cols-3 gap-4">
              <div className="bg-slate-700 rounded p-4">
                <p className="text-slate-400 text-sm">P/E Ratio</p>
                <p className="text-white font-bold text-lg">{stock.pe}</p>
              </div>
              <div className="bg-slate-700 rounded p-4">
                <p className="text-slate-400 text-sm">D/E Ratio</p>
                <p className="text-white font-bold text-lg">{stock.de}</p>
              </div>
              <div className="bg-slate-700 rounded p-4">
                <p className="text-slate-400 text-sm">ROE</p>
                <p className="text-white font-bold text-lg">{stock.roe}%</p>
              </div>
              <div className="bg-slate-700 rounded p-4">
                <p className="text-slate-400 text-sm">ROA</p>
                <p className="text-white font-bold text-lg">{stock.roa}%</p>
              </div>
              <div className="bg-slate-700 rounded p-4">
                <p className="text-slate-400 text-sm">Current Ratio</p>
                <p className="text-white font-bold text-lg">{stock.currentRatio}</p>
              </div>
              <div className="bg-slate-700 rounded p-4">
                <p className="text-slate-400 text-sm">Dividend Yield</p>
                <p className="text-white font-bold text-lg">{stock.dividendYield}%</p>
              </div>
            </div>
          </div>

          <div className="bg-slate-800 rounded-lg p-6 border border-slate-700">
            <h2 className="text-2xl font-bold text-white mb-4">Operating Cash Flow (Last 3 Years) - ✓ Growing</h2>
            <div className="grid grid-cols-3 gap-4">
              {stock.ocf.map((value, idx) => (
                <div key={idx} className="bg-slate-700 rounded p-4 text-center">
                  <p className="text-slate-400 text-sm">Year {idx + 1}</p>
                  <p className="text-green-400 font-bold text-lg">₹{value}Cr</p>
                </div>
              ))}
            </div>
          </div>

          <div className="bg-slate-800 rounded-lg p-6 border border-slate-700">
            <h2 className="text-2xl font-bold text-white mb-4">Performance Returns</h2>
            <div className="grid grid-cols-2 md:grid-cols-4 gap-4">
              <div className="bg-slate-700 rounded p-4">
                <p className="text-slate-400 text-sm">1Y Return</p>
                <p className={`font-bold text-lg ${stock.returns['1y'] >= 0 ? 'text-green-400' : 'text-red-400'}`}>
                  {stock.returns['1y']}%
                </p>
              </div>
              <div className="bg-slate-700 rounded p-4">
                <p className="text-slate-400 text-sm">3Y Return</p>
                <p className="text-green-400 font-bold text-lg">{stock.returns['3y']}%</p>
              </div>
              <div className="bg-slate-700 rounded p-4">
                <p className="text-slate-400 text-sm">5Y Return</p>
                <p className="text-green-400 font-bold text-lg">{stock.returns['5y']}%</p>
              </div>
              <div className="bg-slate-700 rounded p-4">
                <p className="text-slate-400 text-sm">YTD Return</p>
                <p className={`font-bold text-lg ${stock.returns['ytd'] >= 0 ? 'text-green-400' : 'text-red-400'}`}>
                  {stock.returns['ytd']}%
                </p>
              </div>
            </div>
          </div>
        </div>
      )}

      {/* Institutional Tab */}
      {activeTab === 'institutional' && (
        <div className="space-y-6">
          <div className="bg-slate-800 rounded-lg p-6 border border-slate-700">
            <h2 className="text-2xl font-bold text-white mb-4">FII Holdings - ✓ Increasing</h2>
            <div className="grid grid-cols-3 gap-4 mb-4">
              {stock.fii.map((value, idx) => (
                <div key={idx} className="bg-slate-700 rounded p-4 text-center">
                  <p className="text-slate-400 text-sm">Q{3-idx}</p>
                  <p className="text-blue-400 font-bold text-lg">{value}%</p>
                </div>
              ))}
            </div>
            <div className="bg-green-900 border border-green-700 rounded p-4 text-green-100">
              <p className="font-semibold">Trend: {stock.fiiChange} increase in latest quarter</p>
            </div>
          </div>

          <div className="bg-slate-800 rounded-lg p-6 border border-slate-700">
            <h2 className="text-2xl font-bold text-white mb-4">DII Holdings - ✓ Increasing</h2>
            <div className="grid grid-cols-3 gap-4 mb-4">
              {stock.dii.map((value, idx) => (
                <div key={idx} className="bg-slate-700 rounded p-4 text-center">
                  <p className="text-slate-400 text-sm">Q{3-idx}</p>
                  <p className="text-blue-400 font-bold text-lg">{value}%</p>
                </div>
              ))}
            </div>
            <div className="bg-green-900 border border-green-700 rounded p-4 text-green-100">
              <p className="font-semibold">Trend: {stock.diiChange} increase in latest quarter</p>
            </div>
          </div>
        </div>
      )}

      {/* News Tab */}
      {activeTab === 'news' && (
        <div className="space-y-4">
          <h2 className="text-2xl font-bold text-white mb-4">Recent News & Events</h2>
          {stock.news.map((item, idx) => (
            <div key={idx} className="bg-slate-800 rounded-lg p-6 border border-slate-700">
              <div className="flex justify-between items-start mb-2">
                <h3 className="text-white font-bold text-lg">{item.title}</h3>
                <span className="text-slate-400 text-sm">{item.date}</span>
              </div>
              <div className="flex gap-3 items-center">
                <span className={`px-3 py-1 rounded-full text-sm font-semibold ${getSentimentColor(item.sentiment)}`}>
                  {item.sentiment}
                </span>
                <span className="text-slate-400 text-sm">Impact: {item.impact}</span>
              </div>
            </div>
          ))}
        </div>
      )}

      {/* Concall Tab */}
      {activeTab === 'concall' && (
        <div className="space-y-6">
          <div className="bg-slate-800 rounded-lg p-6 border border-slate-700">
            <h2 className="text-2xl font-bold text-white mb-4">Conference Call Information</h2>
            <div className="bg-slate-700 rounded p-4 mb-6">
              <p className="text-slate-400 text-sm">Next Scheduled Call</p>
              <p className="text-white font-bold text-lg">{stock.concall.nextDate}</p>
            </div>
            <div className="bg-slate-700 rounded p-4 mb-6">
              <p className="text-slate-400 text-sm mb-2">Recent Concall Summary</p>
              <p className="text-white">{stock.concall.recentSummary}</p>
            </div>
            <div>
              <p className="text-slate-400 text-sm mb-3">Key Highlights</p>
              <ul className="space-y-2">
                {stock.concall.highlights.map((h, idx) => (
                  <li key={idx} className="text-white flex items-center gap-2">
                    <CheckCircle className="w-5 h-5 text-green-400" />
                    {h}
                  </li>
                ))}
              </ul>
            </div>
          </div>
        </div>
      )}

      {/* SWOT Tab */}
      {activeTab === 'swot' && (
        <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
          {/* Strengths */}
          <div className="bg-green-900 border border-green-700 rounded-lg p-6">
            <h3 className="text-xl font-bold text-green-100 mb-4">Strengths</h3>
            <ul className="space-y-3">
              {stock.swot.strengths.map((item, idx) => (
                <li key={idx} className="text-green-100 flex gap-3">
                  <span className="text-green-400 font-bold">•</span>
                  {item}
                </li>
              ))}
            </ul>
          </div>

          {/* Weaknesses */}
          <div className="bg-red-900 border border-red-700 rounded-lg p-6">
            <h3 className="text-xl font-bold text-red-100 mb-4">Weaknesses</h3>
            <ul className="space-y-3">
              {stock.swot.weaknesses.map((item, idx) => (
                <li key={idx} className="text-red-100 flex gap-3">
                  <span className="text-red-400 font-bold">•</span>
                  {item}
                </li>
              ))}
            </ul>
          </div>

          {/* Opportunities */}
          <div className="bg-blue-900 border border-blue-700 rounded-lg p-6">
            <h3 className="text-xl font-bold text-blue-100 mb-4">Opportunities</h3>
            <ul className="space-y-3">
              {stock.swot.opportunities.map((item, idx) => (
                <li key={idx} className="text-blue-100 flex gap-3">
                  <span className="text-blue-400 font-bold">•</span>
                  {item}
                </li>
              ))}
            </ul>
          </div>

          {/* Threats */}
          <div className="bg-orange-900 border border-orange-700 rounded-lg p-6">
            <h3 className="text-xl font-bold text-orange-100 mb-4">Threats</h3>
            <ul className="space-y-3">
              {stock.swot.threats.map((item, idx) => (
                <li key={idx} className="text-orange-100 flex gap-3">
                  <span className="text-orange-400 font-bold">•</span>
                  {item}
                </li>
              ))}
            </ul>
          </div>
        </div>
      )}

      {/* Rating Tab */}
      {activeTab === 'rating' && (
        <div className="space-y-6">
          <div className="bg-slate-800 rounded-lg p-8 border border-slate-700 text-center">
            <h2 className="text-2xl font-bold text-white mb-6">Overall Rating</h2>
            <div className={`${getRatingColor(stock.rating)} rounded-full w-40 h-40 mx-auto flex items-center justify-center mb-6`}>
              <span className="text-6xl font-bold text-white">{stock.rating}</span>
            </div>
            <p className="text-3xl font-bold text-white mb-2">{getRatingLabel(stock.rating)}</p>
            <p className="text-slate-400">Rating updated: Today</p>
          </div>

          <div className="bg-slate-800 rounded-lg p-6 border border-slate-700">
            <h3 className="text-xl font-bold text-white mb-4">Rating Justification</h3>
            <p className="text-slate-300 mb-4">{stock.ratingJustification}</p>
            <div className="grid grid-cols-1 md:grid-cols-2 gap-4 mt-4">
              <div className="bg-slate-700 rounded p-4">
                <p className="text-slate-400 text-sm">Risk Level</p>
                <p className="text-white font-bold">{stock.riskLevel}</p>
              </div>
              <div className="bg-slate-700 rounded p-4">
                <p className="text-slate-400 text-sm">Time Horizon</p>
                <p className="text-white font-bold">{stock.timeHorizon}</p>
              </div>
            </div>
          </div>

          <div className="bg-slate-800 rounded-lg p-6 border border-slate-700">
            <h3 className="text-xl font-bold text-white mb-4">Best For</h3>
            <ul className="space-y-2">
              {stock.bestFor.map((type, idx) => (
                <li key={idx} className="text-white flex items-center gap-2">
                  <CheckCircle className="w-5 h-5 text-cyan-400" />
                  {type}
                </li>
              ))}
            </ul>
          </div>

          <div className="bg-amber-900 border border-amber-700 rounded-lg p-4">
            <p className="text-amber-100 flex gap-2">
              <AlertCircle className="w-5 h-5 flex-shrink-0" />
              <span><strong>Disclaimer:</strong> This is for informational purposes only and not investment advice. Consult your financial advisor before investing.</span>
            </p>
          </div>
        </div>
      )}
    </div>
  </div>
);
```

}

return (
<div className="min-h-screen bg-gradient-to-br from-slate-950 via-slate-900 to-slate-950">
{/* Header */}
<header className="bg-slate-900 border-b border-slate-700 shadow-xl">
<div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
<h1 className="text-5xl font-bold text-white mb-2">
StockScreen <span className="text-cyan-400">AI</span>
</h1>
<p className="text-slate-400 text-lg">Intelligent Stock Recommendations Based on Fundamental Criteria</p>
</div>
</header>

```
  {/* Screening Criteria */}
  <section className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
    <div className="bg-slate-800 rounded-lg p-8 border border-slate-700 shadow-lg">
      <h2 className="text-2xl font-bold text-white mb-6">Active Screening Criteria</h2>
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
        <div className="bg-slate-700 rounded p-4 border-l-4 border-green-500">
          <div className="flex items-center gap-2 mb-2">
            <CheckCircle className="w-5 h-5 text-green-400" />
            <p className="text-slate-300">P/E Ratio</p>
          </div>
          <p className="text-white font-bold">Less than 15</p>
        </div>
        <div className="bg-slate-700 rounded p-4 border-l-4 border-green-500">
          <div className="flex items-center gap-2 mb-2">
            <CheckCircle className="w-5 h-5 text-green-400" />
            <p className="text-slate-300">Debt-to-Equity</p>
          </div>
          <p className="text-white font-bold">Less than 0.5</p>
        </div>
        <div className="bg-slate-700 rounded p-4 border-l-4 border-green-500">
          <div className="flex items-center gap-2 mb-2">
            <CheckCircle className="w-5 h-5 text-green-400" />
            <p className="text-slate-300">Operating Cash Flow</p>
          </div>
          <p className="text-white font-bold">Growing (3 years)</p>
        </div>
        <div className="bg-slate-700 rounded p-4 border-l-4 border-green-500">
          <div className="flex items-center gap-2 mb-2">
            <CheckCircle className="w-5 h-5 text-green-400" />
            <p className="text-slate-300">Market Cap</p>
          </div>
          <p className="text-white font-bold">Large, Mid, Small Cap</p>
        </div>
        <div className="bg-slate-700 rounded p-4 border-l-4 border-green-500">
          <div className="flex items-center gap-2 mb-2">
            <CheckCircle className="w-5 h-5 text-green-400" />
            <p className="text-slate-300">FII Holdings</p>
          </div>
          <p className="text-white font-bold">Increasing (Recent Q)</p>
        </div>
        <div className="bg-slate-700 rounded p-4 border-l-4 border-green-500">
          <div className="flex items-center gap-2 mb-2">
            <CheckCircle className="w-5 h-5 text-green-400" />
            <p className="text-slate-300">DII Holdings</p>
          </div>
          <p className="text-white font-bold">Increasing (Recent Q)</p>
        </div>
      </div>
      <div className="mt-6 text-slate-300 text-sm">
        <p>📊 <strong>{filteredStocks.length} stocks</strong> currently meet all criteria</p>
        <p className="text-slate-500 text-xs mt-2">Data updated: Today at 3:30 PM IST</p>
      </div>
    </div>
  </section>

  {/* Sorting */}
  <section className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6">
    <div className="flex items-center gap-3">
      <label className="text-white font-semibold">Sort by:</label>
      <select
        value={sortBy}
        onChange={(e) => setSortBy(e.target.value)}
        className="bg-slate-800 border border-slate-700 text-white rounded px-4 py-2 focus:outline-none focus:border-cyan-400"
      >
        <option value="rating">Rating (High to Low)</option>
        <option value="pe">P/E Ratio (Low to High)</option>
        <option value="fii">FII Increase</option>
      </select>
    </div>
  </section>

  {/* Stock Grid */}
  <section className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8 pb-16">
    <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      {filteredStocks.map(stock => (
        <div
          key={stock.id}
          onClick={() => setSelectedStock(stock)}
          className="bg-slate-800 border border-slate-700 rounded-lg p-6 hover:border-cyan-400 hover:shadow-lg hover:shadow-cyan-400/20 transition-all cursor-pointer group"
        >
          <div className="flex justify-between items-start mb-4">
            <div>
              <h3 className="text-xl font-bold text-white group-hover:text-cyan-400 transition-colors">{stock.name}</h3>
              <p className="text-slate-400 text-sm">{stock.sector}</p>
            </div>
            <div className={`${getRatingColor(stock.rating)} rounded-full w-12 h-12 flex items-center justify-center`}>
              <span className="text-white font-bold text-lg">{stock.rating}</span>
            </div>
          </div>

          <div className="space-y-3 mb-4">
            <div className="flex justify-between">
              <span className="text-slate-400">Price</span>
              <span className="text-white font-bold">₹{stock.price}</span>
            </div>
            <div className="flex justify-between">
              <span className="text-slate-400">P/E Ratio</span>
              <span className="text-green-400 font-bold">{stock.pe} ✓</span>
            </div>
            <div className="flex justify-between">
              <span className="text-slate-400">D/E Ratio</span>
              <span className="text-green-400 font-bold">{stock.de} ✓</span>
            </div>
            <div className="flex justify-between">
              <span className="text-slate-400">Market Cap</span>
              <span className="text-white font-semibold text-sm">{stock.marketCap}</span>
            </div>
          </div>

          <div className="space-y-2 mb-4 text-sm">
            <div className="flex items-center gap-2 text-blue-400">
              {parseFloat(stock.fiiChange) > 0 ? <TrendingUp className="w-4 h-4" /> : <TrendingDown className="w-4 h-4" />}
              FII: {stock.fiiChange}
            </div>
            <div className="flex items-center gap-2 text-blue-400">
              {parseFloat(stock.diiChange) > 0 ? <TrendingUp className="w-4 h-4" /> : <TrendingDown className="w-4 h-4" />}
              DII: {stock.diiChange}
            </div>
          </div>

          <button className="w-full bg-cyan-600 hover:bg-cyan-700 text-white font-bold py-2 rounded transition-colors">
            View Details →
          </button>
        </div>
      ))}
    </div>
  </section>

  {/* Footer */}
  <footer className="bg-slate-900 border-t border-slate-700 mt-8">
    <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6 text-center text-slate-400 text-sm">
      <p>⚠️ For informational purposes only. Not investment advice. Consult your financial advisor.</p>
      <p className="mt-2">© 2024 StockScreenAI. All rights reserved.</p>
    </div>
  </footer>
</div>
```

);
};

export default StockRecommendationSite;