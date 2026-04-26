SyncQ Dashboard Components

Here are the exact HTML structures for the requested dashboard modules based on your SaaS design.

1. Multi-Layer Engagement Telemetry

<!-- Middle Row: Interactive Trend Graph -->
<div class="panel rounded-xl p-5 flex-1 min-h-[300px] flex flex-col">
  <div class="flex justify-between items-start mb-4">
    <div>
      <h3 class="text-sm font-bold text-white flex items-center gap-2">Multi-Layer Engagement Telemetry</h3>
      <p class="text-[10px] text-slate-500 mt-1">Cross-referencing global engagement vs attendance vs drop-off rates.</p>
    </div>
    <!-- Graph Layer Toggles -->
    <div class="flex gap-2 bg-[#050914] p-1 rounded-lg border border-white/5">
      <button onclick="toggleGraph('layer-eng')" class="px-2 py-1 rounded bg-brand-primary/20 border border-brand-primary/30 text-brand-primary text-[9px] font-bold flex items-center gap-1 transition-colors" id="btn-layer-eng">
        <div class="w-2 h-2 rounded-full bg-brand-primary"></div> Engagement
      </button>
      <button onclick="toggleGraph('layer-att')" class="px-2 py-1 rounded bg-brand-success/20 border border-brand-success/30 text-brand-success text-[9px] font-bold flex items-center gap-1 transition-colors" id="btn-layer-att">
        <div class="w-2 h-2 rounded-full bg-brand-success"></div> Attendance
      </button>
      <button onclick="toggleGraph('layer-drop')" class="px-2 py-1 rounded bg-brand-danger/20 border border-brand-danger/30 text-brand-danger text-[9px] font-bold flex items-center gap-1 transition-colors" id="btn-layer-drop">
        <div class="w-2 h-2 rounded-full bg-brand-danger"></div> Drop-off
      </button>
    </div>
  </div>
  
  <div class="flex-1 relative w-full overflow-hidden cursor-crosshair group">
    <!-- Custom SVG Multi-Line Chart -->
    <svg class="w-full h-full" viewBox="0 0 1000 300" preserveAspectRatio="none">
      <!-- Grid lines -->
      <g stroke="rgba(255,255,255,0.05)" stroke-width="1">
        <line x1="0" y1="50" x2="1000" y2="50" />
        <line x1="0" y1="150" x2="1000" y2="150" />
        <line x1="0" y1="250" x2="1000" y2="250" />
      </g>
      
      <!-- Layer 1: Engagement (Area + Line) -->
      <g id="layer-eng" class="graph-path">
        <polygon points="0,300 0,180 100,160 200,190 300,140 400,150 500,240 600,120 700,100 800,130 900,90 1000,60 1000,300" fill="url(#grad-blue)" />
        <polyline points="0,180 100,160 200,190 300,140 400,150 500,240 600,120 700,100 800,130 900,90 1000,60" fill="none" stroke="#3B82F6" stroke-width="3" filter="drop-shadow(0 0 8px rgba(59,130,246,0.6))" />
      </g>

      <!-- Layer 2: Attendance (Line) -->
      <g id="layer-att" class="graph-path">
        <polyline points="0,220 100,210 200,230 300,200 400,210 500,260 600,180 700,170 800,190 900,150 1000,140" fill="none" stroke="#10B981" stroke-width="2" filter="drop-shadow(0 0 6px rgba(16,185,129,0.5))" stroke-dasharray="6,4" />
      </g>

      <!-- Layer 3: Drop-off (Line) -->
      <g id="layer-drop" class="graph-path">
        <polyline points="0,280 100,285 200,270 300,275 400,280 500,180 600,260 700,270 800,250 900,260 1000,275" fill="none" stroke="#F43F5E" stroke-width="2" filter="drop-shadow(0 0 6px rgba(244,63,94,0.5))" />
      </g>

      <!-- AI Annotation specific to the dip at x=500 -->
      <g class="transition-opacity duration-300 opacity-70 group-hover:opacity-100">
        <line x1="500" y1="240" x2="500" y2="60" stroke="#F59E0B" stroke-width="1" stroke-dasharray="4,4" />
        <circle cx="500" cy="240" r="6" fill="#F59E0B" class="animate-pulse" />
        <circle cx="500" cy="240" r="12" fill="none" stroke="#F59E0B" opacity="0.5" />
        <!-- Tooltip box simulated -->
        <rect x="430" y="20" w="140" h="40" rx="4" fill="rgba(11,18,33,0.9)" stroke="#F59E0B" stroke-width="1" />
        <text x="500" y="44" fill="#F59E0B" font-size="10" font-weight="bold" font-family="Inter" text-anchor="middle">⚠️ Midsem Dip Detected</text>
      </g>

      <defs>
        <linearGradient id="grad-blue" x1="0" x2="0" y1="0" y2="1">
          <stop offset="0%" stop-color="rgba(59,130,246,0.4)" />
          <stop offset="100%" stop-color="rgba(59,130,246,0)" />
        </linearGradient>
      </defs>
    </svg>
  </div>
</div>


2. Campus Activity Heat Map

<!-- Dynamic Heatmap -->
<div class="panel rounded-xl p-5 lg:col-span-2">
  <div class="flex justify-between items-center mb-4">
    <h3 class="text-sm font-bold text-white flex items-center gap-2">Campus Activity Heatmap</h3>
    <div class="text-[9px] text-slate-500 flex items-center gap-1 border border-white/5 rounded px-2 py-1">
      Less <span class="w-2 h-2 bg-[#1E293B] rounded-[2px] ml-1"></span><span class="w-2 h-2 bg-brand-primary/40 rounded-[2px]"></span><span class="w-2 h-2 bg-brand-primary/70 rounded-[2px]"></span><span class="w-2 h-2 bg-brand-neon rounded-[2px] shadow-[0_0_5px_#38BDF8] mr-1"></span> More
    </div>
  </div>
  
  <div class="w-full overflow-x-auto custom-scrollbar pb-2">
    <!-- Generate a 53-week GitHub-style heatmap structure using grid -->
    <div class="grid grid-rows-7 grid-flow-col gap-1 w-max" id="heatmap-container">
      <!-- Javascript will inject 365 squares here -->
    </div>
  </div>
</div>

<script>
  // Required JS to generate the heatmap blocks
  function generateHeatmap() {
    const container = document.getElementById('heatmap-container');
    if(!container) return;
    
    const colors = ['bg-[#1E293B]', 'bg-brand-primary/40', 'bg-brand-primary/70', 'bg-brand-neon shadow-[0_0_5px_#38BDF8]'];
    
    let html = '';
    for(let i=0; i<364; i++) {
      let rand = Math.random();
      let level = 0;
      if(rand > 0.6) level = 1;
      if(rand > 0.85) level = 2;
      if(rand > 0.95) level = 3;
      
      html += `<div class="w-2.5 h-2.5 rounded-[2px] ${colors[level]} cursor-pointer hover:ring-1 hover:ring-white transition-all duration-200" title="Activity level: ${level}"></div>`;
    }
    container.innerHTML = html;
  }
  generateHeatmap();
</script>


3. Top Influencers (Leaderboard)

<!-- Leaderboard -->
<div class="panel rounded-xl p-5 flex flex-col">
  <div class="flex justify-between items-center mb-4">
    <h3 class="text-sm font-bold text-white">Top Influencers</h3>
    <i data-lucide="award" class="w-4 h-4 text-brand-warning"></i>
  </div>
  <div class="flex flex-col gap-3 flex-1">
    <div class="flex items-center justify-between p-2 rounded-lg bg-white/[0.02] border border-white/5 hover:bg-white/5 cursor-pointer transition-colors group">
      <div class="flex items-center gap-3">
        <span class="text-brand-warning font-bold text-xs w-4">#1</span>
        <div class="w-7 h-7 rounded-full bg-gradient-to-tr from-brand-warning to-rose-500 flex items-center justify-center text-[9px] font-bold text-white shadow-[0_0_10px_rgba(245,158,11,0.3)] group-hover:scale-110 transition-transform">AS</div>
        <div class="flex flex-col">
          <span class="text-xs font-bold text-slate-200">Ayush Sanger</span>
          <span class="text-[9px] text-slate-500">FITSOC Core</span>
        </div>
      </div>
      <span class="text-brand-success text-[10px] font-bold">+142 pts</span>
    </div>
    
    <div class="flex items-center justify-between p-2 rounded-lg bg-white/[0.02] border border-white/5 hover:bg-white/5 cursor-pointer transition-colors group">
      <div class="flex items-center gap-3">
        <span class="text-slate-400 font-bold text-xs w-4">#2</span>
        <div class="w-7 h-7 rounded-full bg-gradient-to-tr from-slate-400 to-slate-600 flex items-center justify-center text-[9px] font-bold text-white group-hover:scale-110 transition-transform">RK</div>
        <div class="flex flex-col">
          <span class="text-xs font-bold text-slate-200">Rahul K.</span>
          <span class="text-[9px] text-slate-500">Coding Club</span>
        </div>
      </div>
      <span class="text-brand-success text-[10px] font-bold">+98 pts</span>
    </div>

    <div class="flex items-center justify-between p-2 rounded-lg bg-white/[0.02] border border-white/5 hover:bg-white/5 cursor-pointer transition-colors group">
      <div class="flex items-center gap-3">
        <span class="text-slate-500 font-bold text-xs w-4">#3</span>
        <div class="w-7 h-7 rounded-full bg-gradient-to-tr from-brand-primary to-purple-500 flex items-center justify-center text-[9px] font-bold text-white group-hover:scale-110 transition-transform">SJ</div>
        <div class="flex flex-col">
          <span class="text-xs font-bold text-slate-200">Sneha J.</span>
          <span class="text-[9px] text-slate-500">Debate Soc</span>
        </div>
      </div>
      <span class="text-brand-success text-[10px] font-bold">+76 pts</span>
    </div>
  </div>
</div>


4. Club Performance Matrix

<!-- Club Performance Matrix -->
<div class="panel rounded-xl p-5 flex-1 flex flex-col relative overflow-hidden">
   <h3 class="text-sm font-bold text-white mb-1">Club Performance Matrix</h3>
   <p class="text-[10px] text-slate-500 mb-6">X-Axis: Event Participation Volume | Y-Axis: Member Retention Rate</p>
   
   <div class="flex-1 relative w-full border border-white/10 bg-[#050914] rounded-lg min-h-[300px]">
     <!-- Crosshairs -->
     <div class="absolute left-1/2 top-0 bottom-0 w-px bg-white/10"></div>
     <div class="absolute top-1/2 left-0 right-0 h-px bg-white/10"></div>

     <!-- Labels -->
     <span class="absolute top-2 left-1/2 -translate-x-1/2 text-[9px] font-bold text-brand-success uppercase tracking-widest bg-[#050914] px-2 z-10">High Retention</span>
     <span class="absolute bottom-2 left-1/2 -translate-x-1/2 text-[9px] font-bold text-brand-danger uppercase tracking-widest bg-[#050914] px-2 z-10">Low Retention</span>
     <span class="absolute left-2 top-1/2 -translate-y-1/2 -rotate-90 text-[9px] font-bold text-slate-500 uppercase tracking-widest bg-[#050914] px-2 z-10">Niche / Low Vol</span>
     <span class="absolute right-2 top-1/2 -translate-y-1/2 rotate-90 text-[9px] font-bold text-brand-primary uppercase tracking-widest bg-[#050914] px-2 z-10">Mass / High Vol</span>

     <!-- Quadrant Backgrounds (Subtle) -->
     <div class="absolute top-0 right-0 w-1/2 h-1/2 bg-brand-success/5 border-b border-l border-brand-success/20"></div> <!-- Stars -->
     <div class="absolute bottom-0 right-0 w-1/2 h-1/2 bg-brand-warning/5 border-t border-l border-brand-warning/20"></div> <!-- Leaky Bucket -->
     <div class="absolute bottom-0 left-0 w-1/2 h-1/2 bg-brand-danger/5 border-t border-r border-brand-danger/20"></div> <!-- Risk -->

     <!-- Data Points (Clubs) -->
     <!-- Star Quad -->
     <div class="absolute w-4 h-4 rounded-full bg-brand-primary border-2 border-[#050914] shadow-[0_0_15px_#3B82F6] cursor-pointer hover:scale-150 transition-transform z-20 group" style="top: 20%; right: 20%;">
       <span class="absolute left-6 top-0 text-[10px] font-bold text-white whitespace-nowrap opacity-0 group-hover:opacity-100 transition-opacity bg-[#111827] px-2 py-1 rounded border border-white/10">Coding Club</span>
     </div>
     <div class="absolute w-5 h-5 rounded-full bg-brand-success border-2 border-[#050914] shadow-[0_0_15px_#10B981] cursor-pointer hover:scale-150 transition-transform z-20 group" style="top: 30%; right: 35%;">
       <span class="absolute left-7 top-0 text-[10px] font-bold text-white whitespace-nowrap opacity-0 group-hover:opacity-100 transition-opacity bg-[#111827] px-2 py-1 rounded border border-white/10">FITSOC</span>
     </div>

     <!-- Leaky Bucket Quad -->
     <div class="absolute w-3 h-3 rounded-full bg-brand-warning border-2 border-[#050914] shadow-[0_0_10px_#F59E0B] cursor-pointer hover:scale-150 transition-transform z-20 group animate-pulse" style="bottom: 30%; right: 25%;">
       <span class="absolute left-5 top-0 text-[10px] font-bold text-white whitespace-nowrap opacity-0 group-hover:opacity-100 transition-opacity bg-[#111827] px-2 py-1 rounded border border-white/10 border-l-brand-warning">Debate Soc (Warning)</span>
     </div>

     <!-- Niche Quad -->
     <div class="absolute w-2 h-2 rounded-full bg-slate-400 border-2 border-[#050914] cursor-pointer hover:scale-150 transition-transform z-20 group" style="top: 25%; left: 30%;">
       <span class="absolute left-4 top-0 text-[10px] font-bold text-white whitespace-nowrap opacity-0 group-hover:opacity-100 transition-opacity bg-[#111827] px-2 py-1 rounded border border-white/10">Chess Club</span>
     </div>
   </div>
</div>


5. Engagement Funnel

<!-- Engagement Funnel -->
<div class="panel rounded-xl p-5 flex flex-col">
  <h3 class="text-sm font-bold text-white mb-4 flex justify-between items-center">
    Engagement Funnel <i data-lucide="filter" class="w-4 h-4 text-slate-500"></i>
  </h3>
  <div class="flex-1 flex flex-col justify-center gap-2 items-center w-full">
    <!-- CSS simulated funnel -->
    <div class="w-[95%] h-10 bg-brand-primary/20 border border-brand-primary/40 rounded flex items-center justify-between px-4 cursor-pointer hover:bg-brand-primary/30 transition-colors shadow-[0_0_10px_rgba(59,130,246,0.1)]">
      <span class="text-[10px] font-bold text-brand-neon uppercase tracking-wider">Total Enrolled</span>
      <span class="text-sm font-bold text-white">15,000</span>
    </div>
    <div class="w-[75%] h-10 bg-brand-success/20 border border-brand-success/40 rounded flex items-center justify-between px-4 cursor-pointer hover:bg-brand-success/30 transition-colors shadow-[0_0_10px_rgba(16,185,129,0.1)]">
      <span class="text-[10px] font-bold text-brand-success uppercase tracking-wider">Active (>1 Event)</span>
      <span class="text-sm font-bold text-white">11,240</span>
    </div>
    <div class="w-[45%] h-10 bg-brand-warning/20 border border-brand-warning/40 rounded flex items-center justify-between px-4 cursor-pointer hover:bg-brand-warning/30 transition-colors shadow-[0_0_10px_rgba(245,158,11,0.1)]">
      <span class="text-[10px] font-bold text-brand-warning uppercase tracking-wider">Passive (Watchlist)</span>
      <span class="text-sm font-bold text-white">2,850</span>
    </div>
    <div class="w-[25%] h-10 bg-brand-danger/20 border border-brand-danger/40 rounded flex items-center justify-between px-4 cursor-pointer hover:bg-brand-danger/30 transition-colors shadow-[0_0_15px_rgba(244,63,94,0.3)] animate-pulse-slow">
      <span class="text-[10px] font-bold text-brand-danger uppercase tracking-wider">At Risk</span>
      <span class="text-sm font-bold text-white">910</span>
    </div>
  </div>
</div>

