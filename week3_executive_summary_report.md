# Week 3: Executive Summary Report

This executive summary integrates our data engineering and statistical findings across 4,757 London neighbourhoods (LSOAs) to explain how safety, deprivation, and public transport accessibility drive property values. All comparisons are grounded in robust **quintile divisions** (top 20% vs. bottom 20% groups).

---

## 1. Executive Summary of Key Findings

1. **Deprivation is the Primary Property Value Driver:**
   - Property prices in low-deprivation areas (bottom 20% of IMD scores) average **£865,127** (median: **£700,000**), compared to **£456,149** (median: **£420,668**) in high-deprivation areas (top 20%). Deprivation has the strongest overall correlation with house prices ($r = -0.40^{***}$).
2. **Safety and Crime Composition Matter Over Total Volume:**
   - The overall association between total crime and property value is heavily confounded by central London commercial hotspots like Westminster. 
   - When Westminster is excluded, we observe a highly significant negative impact of crime on property values (Welch's $t = 9.96, p < 0.001$), which becomes even stronger when both Westminster and Kensington & Chelsea are excluded ($t = 14.50, p < 0.001$).
   - Multiple regression models show that **Violence Against The Person** has the most consistent depressing effect on property values, whereas **Theft** correlates positively with land value due to its concentration in premium commercial and shopping hubs.
3. **Transport Connectivity Adds a Premium:**
   - Good transport accessibility (PTAI) is positively associated with property values (r = 0.181, p < 0.001). 
   - Neighborhoods in the top 20% of transport accessibility command average property prices of **£746,201** (median: **£592,575**), compared to **£589,399** (median: **£500,000**) in the bottom 20%. Each one-point increase in PTAI score adds approximately **£5,834** to average property values.

---

## 2. Spatial Autocorrelation & Spillover Effects

An important analytical enhancement is the qualitative consideration of **spatial autocorrelation**—the principle that geographic proximity between neighbouring LSOAs creates localized price and crime spillover effects.
- **Price Spillovers:** Property prices are not isolated. High-value neighbourhoods (such as those in Kensington & Chelsea) exert a positive spatial spillover effect, raising the property values of bordering LSOAs (e.g. in Hammersmith or Brent) due to proximity and demand displacement.
- **Crime Spillovers:** Similarly, criminal activity is not restricted to administrative boundaries. High-crime hubs, particularly violent hotspots, create localized safety risks that spill over into adjacent LSOAs, depressing housing demand and prices across entire districts, rather than just within the immediate neighborhood.

---

## 3. Actionable Stakeholder Recommendations

### For Homebuyers
- **Prioritize Specific Safety Metrics, Not Total Crime:** Ignore high "total crime" figures in commercial centers when house hunting. Focus on the local rate of **Violence Against The Person** as a proxy for safety.
- **Identify "Transit Borders":** Look for residential neighbourhoods located just outside premium high-PTAL zones. These areas benefit from proximity to transport hubs without the high price premiums.
- **Target Low-Deprivation Clusters:** Look for neighborhoods that border low-deprivation areas, as positive spatial price spillovers are likely to support property values over time.

### For Property Investors
- **Target Transport Regeneration Zones:** Identify high-deprivation areas where major transport infrastructure expansions (similar to the Elizabeth Line) are planned. The transition from a low-PTAL to high-PTAL quintile will drive significant capital appreciation.
- **Monitor Crime Composition Trends:** Look for districts where violent crime is falling, even if property theft remains stable. Reductions in violent crime are strong precursors to residential regeneration.

### For Local Councils & Urban Planners
- **Implement financially costed safety upgrades:** Pair transport investments with safety measures like smart lighting and CCTV, especially in poorer areas.
- **Address Spillover Effects Collaboratively:** Since crime and housing demand spill over across boundaries, neighbouring local councils should coordinate safety patrols and streetscape improvements to maximize regional regeneration.

---

## 4. Interactive Tableau Dashboard

To explore the spatial relationships between house prices, crime categories, deprivation, and transport accessibility across London, you can view our interactive dashboard:
[Neighbourhood Characteristics and House Prices in London Dashboard](https://public.tableau.com/app/profile/raquel.cancho.gasulla/viz/NeighbourhoodCharacteristicsandHousePricesinLondon/Dashboard1)
