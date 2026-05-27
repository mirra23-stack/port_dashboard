<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PortMaintain CMMS Platform</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght=400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        :root {
            --bg-main: #c47b7b;
            --sidebar-bg: #5a3535;
            --sidebar-active: #784a4a;
            --card-bg: #6e4141;
            --panel-bg: rgba(90, 53, 53, 0.4);
            --panel-light-bg: #dca3a3;
            --text-main: #ffffff;
            --text-muted: #e4c5c5;
            --text-dark: #4a2828;
            --badge-yellow: #f1c40f;
            --badge-red: #e74c3c;
            --badge-purple: #9b59b6;
            --badge-green: #2ecc71;
            --badge-pink: #d87093;
            --badge-blue: #3498db;
            --input-bg: rgba(0, 0, 0, 0.2);
            --star-gold: #f39c12;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Inter', sans-serif;
        }

        body {
            background-color: var(--bg-main);
            color: var(--text-main);
            display: flex;
            height: 100vh;
            overflow: hidden;
        }

        /* --- SIDEBAR --- */
        .sidebar {
            width: 260px;
            background-color: var(--sidebar-bg);
            display: flex;
            flex-direction: column;
            padding: 20px 0;
            overflow-y: auto;
            flex-shrink: 0;
        }

        .sidebar-brand {
            padding: 0 20px 20px 20px;
            border-bottom: 1px solid rgba(255,255,255,0.1);
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .brand-icon {
            background: #e74c3c;
            padding: 10px;
            border-radius: 8px;
            font-size: 20px;
            width: 42px;
            height: 42px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .brand-text h1 {
            font-size: 16px;
            font-weight: 700;
            letter-spacing: 0.5px;
        }

        .brand-text span {
            font-size: 11px;
            color: var(--text-muted);
            display: block;
        }

        .user-profile {
            background: rgba(255, 255, 255, 0.1);
            margin: 20px;
            padding: 12px;
            border-radius: 25px;
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .avatar {
            width: 36px;
            height: 36px;
            background: var(--bg-main);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }

        .user-info h2 { font-size: 13px; font-weight: 600; }
        .user-info p { font-size: 11px; color: var(--text-muted); }

        .menu-group { margin-bottom: 25px; }
        .menu-title {
            font-size: 11px;
            font-weight: 700;
            color: var(--text-muted);
            padding: 0 20px;
            margin-bottom: 10px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .menu-item {
            display: flex;
            align-items: center;
            padding: 12px 20px;
            color: var(--text-muted);
            text-decoration: none;
            font-size: 14px;
            font-weight: 500;
            transition: background 0.2s;
            position: relative;
            cursor: pointer;
        }

        .menu-item:hover, .menu-item.active {
            background-color: var(--sidebar-active);
            color: #fff;
        }

        .menu-item i { width: 25px; font-size: 16px; }
        .menu-item .badge {
            position: absolute;
            right: 20px;
            padding: 2px 8px;
            border-radius: 10px;
            font-size: 11px;
            font-weight: 700;
            color: #000;
        }

        .badge.red { background-color: var(--badge-red); color: #fff; }
        .badge.yellow { background-color: var(--badge-yellow); }
        .badge.purple { background-color: var(--badge-purple); color: #fff; }
        .badge.blue { background-color: var(--badge-blue); color: #fff; }

        /* --- LAYOUT WRAPPERS --- */
        .main-content {
            flex-grow: 1;
            padding: 25px;
            overflow-y: auto;
            display: none;
        }

        .main-content.active-view { display: block; }

        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .header h2 {
            font-size: 22px;
            font-weight: 700;
            letter-spacing: 0.5px;
            text-transform: uppercase;
        }

        .live-indicator {
            display: flex;
            align-items: center;
            gap: 6px;
            font-size: 12px;
            font-weight: 600;
        }

        .live-dot {
            width: 8px;
            height: 8px;
            background-color: var(--badge-green);
            border-radius: 50%;
            box-shadow: 0 0 8px var(--badge-green);
        }

        .action-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .filter-tabs { display: flex; gap: 8px; }

        .tab-btn {
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.15);
            color: var(--text-main);
            padding: 8px 16px;
            border-radius: 20px;
            font-size: 13px;
            font-weight: 500;
            cursor: pointer;
        }

        .tab-btn.active, .tab-btn:hover { background: rgba(255, 255, 255, 0.25); }
        .right-actions { display: flex; gap: 10px; }

        .btn-primary {
            background-color: #d84b65;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            font-size: 13px;
            font-weight: 700;
            text-transform: uppercase;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .btn-secondary {
            background-color: rgba(90, 53, 53, 0.6);
            color: white;
            border: 1px solid rgba(255,255,255,0.2);
            padding: 10px 20px;
            border-radius: 8px;
            font-size: 13px;
            font-weight: 700;
            text-transform: uppercase;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        /* --- DASHBOARD ELEMENTS --- */
        .kpi-grid { display: grid; grid-template-columns: repeat(6, 1fr); gap: 15px; margin-bottom: 25px; }
        .kpi-card { background-color: var(--card-bg); border-radius: 8px; padding: 15px; }
        .kpi-title { font-size: 11px; font-weight: 700; text-transform: uppercase; color: var(--text-muted); margin-bottom: 12px; letter-spacing: 0.5px; }
        .kpi-value { font-size: 36px; font-weight: 700; line-height: 1; margin-bottom: 8px; }
        .kpi-subtext { font-size: 11px; color: var(--text-muted); }
        .dashboard-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 20px; margin-bottom: 20px; }
        .widget { background-color: var(--card-bg); border-radius: 8px; overflow: hidden; }
        .widget-header { background-color: rgba(0, 0, 0, 0.15); padding: 15px 20px; display: flex; justify-content: space-between; align-items: center; }
        .widget-title { font-size: 13px; font-weight: 700; text-transform: uppercase; letter-spacing: 0.5px; display: flex; align-items: center; gap: 10px; }
        .widget-count-badge { background: rgba(0, 0, 0, 0.3); width: 22px; height: 22px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 11px; font-weight: bold; }
        .widget-header.purple-badge .widget-count-badge { background-color: var(--badge-purple); }
        .widget-body { padding: 5px 0; }
        .list-row { display: flex; justify-content: space-between; align-items: center; padding: 15px 20px; border-bottom: 1px solid rgba(255, 255, 255, 0.05); }
        .list-row:last-child { border-bottom: none; }
        .row-main-text { font-size: 13px; font-weight: 600; margin-bottom: 4px; }
        .row-sub-text { font-size: 11px; color: var(--text-muted); }

        /* --- DATA TABLES --- */
        .table-panel { border-radius: 12px; padding: 20px; border: 1px solid rgba(255,255,255,0.1); margin-bottom: 20px; }
        .table-panel.dark { background-color: var(--panel-bg); }
        .table-panel.light { background-color: var(--panel-light-bg); color: var(--text-dark); border: 1px solid rgba(0,0,0,0.05); }
        .table-panel.light-dark-mix { background-color: #533030; color: var(--text-main); border: 1px solid rgba(255,255,255,0.08); }
        .table-panel-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; }
        .panel-title { font-size: 14px; font-weight: 700; text-transform: uppercase; letter-spacing: 0.5px; }
        
        .search-container { position: relative; width: 260px; }
        .search-container input {
            width: 100%;
            background: var(--input-bg);
            border: 1px solid rgba(255,255,255,0.15);
            border-radius: 6px;
            padding: 8px 12px 8px 35px;
            color: white;
            font-size: 13px;
        }
        .table-panel.light .search-container input { background: rgba(255, 255, 255, 0.4); border: 1px solid rgba(0, 0, 0, 0.15); color: var(--text-dark); }
        .table-panel.light .search-container input::placeholder { color: #6b4545; }
        .search-container i { position: absolute; left: 12px; top: 50%; transform: translateY(-50%); color: var(--text-muted); font-size: 14px; }
        .table-panel.light .search-container i { color: #6b4545; }

        .wo-table { width: 100%; border-collapse: collapse; text-align: left; }
        .wo-table th { font-size: 11px; text-transform: uppercase; color: var(--text-muted); font-weight: 700; padding: 12px 10px; border-bottom: 1px solid rgba(255, 255, 255, 0.15); letter-spacing: 0.5px; }
        .table-panel.light th { color: #533333; border-bottom: 1px solid rgba(0,0,0,0.12); }
        .table-panel.light-dark-mix th { color: #eecfcf; border-bottom: 1px solid rgba(255,255,255,0.15); }
        .wo-table td { padding: 14px 10px; border-bottom: 1px solid rgba(255, 255, 255, 0.08); font-size: 13px; vertical-align: middle; }
        .table-panel.light td { border-bottom: 1px solid rgba(0,0,0,0.06); }

        .wo-id-cell { font-weight: 600; color: #ff9f9f; }
        .table-panel.light .wo-id-cell { color: #723939; }
        .table-panel.light-dark-mix .wo-id-cell { color: #ffa8a8; }

        .auto-tag {
            display: inline-flex;
            align-items: center;
            gap: 4px;
            background: rgba(231, 76, 60, 0.2);
            border: 1px solid var(--badge-red);
            font-size: 10px;
            text-transform: uppercase;
            font-weight: 700;
            padding: 2px 6px;
            border-radius: 4px;
            margin-top: 4px;
            color: #ffcdd2;
        }
        .table-panel.light .auto-tag { background: rgba(231, 76, 60, 0.15); color: #721c24; }
        .title-subtext { font-size: 11px; color: var(--text-muted); margin-top: 2px; }
        .table-panel.light .title-subtext { color: #5e3f3f; }
        .table-panel.light-dark-mix .title-subtext { color: #dfb2b2; }

        /* --- STATUS BADGES --- */
        .status-tag { font-size: 10px; font-weight: 700; padding: 5px 10px; border-radius: 4px; text-transform: uppercase; display: inline-block; text-align: center; }
        .tag-yellow { background-color: var(--badge-yellow); color: #000; }
        .tag-red { background-color: var(--badge-red); color: #fff; }
        .tag-orange { background-color: #e67e22; color: #fff; }
        .tag-pink { background-color: var(--badge-pink); color: #fff; }
        .tag-green { background-color: var(--badge-green); color: #fff; }
        .tag-dark-red { background-color: #801515; color: #fff; }
        .tag-light-gray { background-color: rgba(255,255,255,0.4); color: #000; }
        .table-panel.light .tag-light-gray { background-color: rgba(0,0,0,0.12); color: var(--text-dark); }
        .tag-muted-border { border: 1px solid rgba(255,255,255,0.4); color: white; background: transparent; font-size: 10px; }
        .table-panel.light .tag-muted-border { border: 1px solid rgba(0,0,0,0.3); color: var(--text-dark); }
        .table-panel.light-dark-mix .tag-muted-border { border: 1px solid rgba(255,255,255,0.25); color: #eed5d5; }
        .tag-black { background-color: #2b2b2b; color: #ffffff; }

        /* --- ACTION INTERFACES --- */
        .action-buttons { display: flex; gap: 5px; }
        .btn-action { border: none; border-radius: 4px; padding: 6px 10px; font-size: 11px; font-weight: 700; text-transform: uppercase; cursor: pointer; color: white; display: inline-flex; align-items: center; justify-content: center; }
        .btn-edit { background: rgba(255, 255, 255, 0.15); border: 1px solid rgba(255,255,255,0.2); }
        .table-panel.light .btn-edit { background: rgba(0, 0, 0, 0.08); border: 1px solid rgba(0,0,0,0.15); color: var(--text-dark); }
        .table-panel.light-dark-mix .btn-edit { background: rgba(255,255,255,0.08); border: 1px solid rgba(255,255,255,0.15); color: white; }
        .btn-check { background-color: rgba(46, 204, 113, 0.3); border: 1px solid var(--badge-green); color: var(--badge-green); }
        .table-panel.light .btn-check { background-color: var(--badge-green); color: white; border: none; }
        .btn-delete { background-color: var(--badge-red); border: none; }
        .btn-qty { background-color: var(--badge-blue); border: none; }

        /* --- IOT TRACKING TILES --- */
        .iot-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; margin-bottom: 25px; }
        .iot-card { background: var(--card-bg); border-radius: 12px; padding: 20px; position: relative; border: 1px solid rgba(255,255,255,0.05); }
        .iot-card-header { display: flex; align-items: center; gap: 12px; margin-bottom: 18px; }
        .iot-icon { width: 40px; height: 40px; border-radius: 8px; display: flex; align-items: center; justify-content: center; font-size: 18px; }
        .iot-icon.orange-bg { background: rgba(241, 196, 15, 0.2); color: var(--badge-yellow); }
        .iot-icon.blue-bg { background: rgba(52, 152, 219, 0.2); color: #3498db; }
        .iot-icon.green-bg { background: rgba(46, 204, 113, 0.2); color: var(--badge-green); }
        .iot-card-title h3 { font-size: 14px; font-weight: 700; }
        .iot-card-title p { font-size: 11px; color: var(--text-muted); }
        .iot-status-dot { position: absolute; top: 20px; right: 20px; width: 10px; height: 10px; border-radius: 50%; }
        .iot-status-dot.green { background: var(--badge-green); box-shadow: 0 0 8px var(--badge-green); }
        .iot-status-dot.red { background: var(--badge-red); box-shadow: 0 0 8px var(--badge-red); }
        
        .iot-metrics-box { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 15px; }
        .metric-subcard { background: rgba(0,0,0,0.15); padding: 10px 12px; border-radius: 6px; }
        .metric-label { font-size: 10px; text-transform: uppercase; color: var(--text-muted); font-weight: 600; margin-bottom: 4px; }
        .metric-val { font-size: 18px; font-weight: 700; color: #ffebbc; }
        .metric-val span { font-size: 12px; color: var(--text-muted); margin-left: 2px; }
        
        .iot-threshold-alert { background: rgba(231, 76, 60, 0.2); border: 1px solid var(--badge-red); padding: 8px 12px; border-radius: 6px; font-size: 11px; font-weight: 600; color: #ffcdd2; display: flex; align-items: center; gap: 6px; }
        .iot-threshold-alert.warning { background: rgba(241, 196, 15, 0.15); border: 1px solid var(--badge-yellow); color: #ffeaa7; }
        .iot-card-footer-time { font-size: 11px; color: var(--text-muted); margin-top: 10px; display: block; }

        /* --- MAP & ZONES VIEW STYLES --- */
        .map-container-panel { background-color: var(--panel-bg); border: 1px solid rgba(255,255,255,0.1); border-radius: 12px; padding: 24px; }
        .map-panel-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 16px; }
        .map-canvas { background-color: rgba(0, 0, 0, 0.25); border-radius: 8px; padding: 40px; min-height: 500px; position: relative; }
        .map-water-label { text-align: center; font-size: 12px; font-weight: 700; letter-spacing: 3px; color: rgba(255, 255, 255, 0.4); text-transform: uppercase; margin-bottom: 40px; }
        .map-grid-layout { display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px; margin-bottom: 24px; }
        .map-zone-block { background-color: rgba(255, 255, 255, 0.15); border: 1px solid rgba(255, 255, 255, 0.2); border-radius: 6px; height: 180px; padding: 16px; display: flex; align-items: center; justify-content: center; text-transform: uppercase; font-weight: 600; font-size: 11px; letter-spacing: 1px; color: rgba(255,255,255,0.7); position: relative; }
        .map-zone-block.yellow-zone { background-color: rgba(241, 196, 15, 0.15); border-color: rgba(241, 196, 15, 0.3); color: #ffeaa7; }
        .map-zone-block.purple-zone { background-color: rgba(155, 89, 182, 0.15); border-color: rgba(155, 89, 182, 0.3); color: #e8dbf1; }
        .absolute-node { position: absolute; background-color: rgba(255, 255, 255, 0.15); border: 1px solid rgba(255, 255, 255, 0.2); border-radius: 6px; padding: 12px; font-size: 10px; font-weight: 700; text-transform: uppercase; letter-spacing: 0.5px; color: rgba(255,255,255,0.7); }
        .powerhouse-node { bottom: 120px; left: 40px; width: 100px; height: 70px; display: flex; align-items: center; justify-content: center; text-align: center; }
        .fueldock-node { top: 140px; right: 15px; width: 110px; height: 65px; display: flex; align-items: center; justify-content: center; background-color: rgba(255, 255, 255, 0.12); }
        .map-footer-legend { background-color: rgba(0, 0, 0, 0.2); margin-top: 20px; padding: 12px 20px; border-radius: 6px; display: flex; justify-content: space-between; align-items: center; font-size: 12px; }
        .legend-items { display: flex; gap: 20px; }
        .legend-item { display: flex; align-items: center; gap: 8px; font-weight: 500; }
        .legend-color { width: 10px; height: 10px; border-radius: 50%; }
        .pulse-alert { animation: mapPulse 2s infinite; }
        @keyframes mapPulse {
            0% { box-shadow: 0 0 0 0 rgba(231, 76, 60, 0.7); }
            70% { box-shadow: 0 0 0 10px rgba(231, 76, 60, 0); }
            100% { box-shadow: 0 0 0 0 rgba(231, 76, 60, 0); }
        }

        /* --- RATINGS SYSTEM --- */
        .stars-container { color: var(--star-gold); font-size: 12px; display: flex; gap: 2px; }

        /* --- PROFILE SUBTEXT SPECIALS --- */
        .sub-email { font-size: 11px; color: #ffe4e4; display: block; margin-top: 1px; font-weight: 400; opacity: 0.8; }
        .table-panel.light .sub-email { color: #5e3f3f; }

        /* --- WO COUNT CONTAINER --- */
        .wo-count-box { font-size: 14px; font-weight: 700; display: inline-block; padding: 2px 8px; border-radius: 4px; text-align: center; }

        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-track { background: rgba(0,0,0,0.05); }
        ::-webkit-scrollbar-thumb { background: rgba(255,255,255,0.2); border-radius: 3px; }
    </style>
</head>
<body>

    <aside class="sidebar">
        <div class="sidebar-brand">
            <div class="brand-icon"><i class="fa-solid fa-anchor"></i></div>
            <div class="brand-text">
                <h1>PORTMAINTAIN</h1>
                <span>CMMS v4</span>
            </div>
        </div>

        <div class="user-profile">
            <div class="avatar">A</div>
            <div class="user-info">
                <h2>Demo User</h2>
                <p>Administrator</p>
            </div>
        </div>

        <div class="menu-group">
            <div class="menu-title">Operations</div>
            <div class="menu-item active" onclick="switchView('dashboard-view', this)"><i class="fa-solid fa-house"></i> Dashboard</div>
            <div class="menu-item" onclick="switchView('workorders-view', this)"><i class="fa-solid fa-file-invoice"></i> Work Orders <span class="badge red">12</span></div>
            <div class="menu-item" onclick="switchView('pm-view', this)"><i class="fa-solid fa-clock-history"></i> Preventive Maint. <span class="badge yellow">4</span></div>
            <div class="menu-item" onclick="switchView('assets-view', this)"><i class="fa-solid fa-gear"></i> Assets</div>
        </div>

        <div class="menu-group">
            <div class="menu-title">IoT & Location</div>
            <div class="menu-item" onclick="switchView('iot-view', this)"><i class="fa-solid fa-tower-broadcast"></i> IoT Monitoring <span class="badge purple">5</span></div>
            <div class="menu-item" onclick="switchView('map-view', this)"><i class="fa-solid fa-map-location-dot"></i> Port Map & Zones</div>
        </div>

        <div class="menu-group">
            <div class="menu-title">Resources</div>
            <div class="menu-item" onclick="switchView('inventory-view', this)"><i class="fa-solid fa-warehouse"></i> Inventory <span class="badge yellow">4</span></div>
            <div class="menu-item" onclick="switchView('technicians-view', this)"><i class="fa-solid fa-users"></i> Technicians</div>
            <div class="menu-item" onclick="switchView('vendors-view', this)"><i class="fa-solid fa-truck"></i> Vendors</div>
        </div>
    </aside>

    <main id="dashboard-view" class="main-content active-view">
        <div class="header">
            <h2>Dashboard</h2>
            <div class="live-indicator"><div class="live-dot"></div> LIVE</div>
        </div>

        <div class="kpi-grid">
            <div class="kpi-card"><div class="kpi-title">Open Work Orders</div><div class="kpi-value">4</div><div class="kpi-subtext">1 In progress</div></div>
            <div class="kpi-card"><div class="kpi-title">Overdue WOs</div><div class="kpi-value">0</div><div class="kpi-subtext">past due date</div></div>
            <div class="kpi-card"><div class="kpi-title">PM Overdue</div><div class="kpi-value">2</div><div class="kpi-subtext">2 due soon</div></div>
            <div class="kpi-card"><div class="kpi-title">IoT Alerts</div><div class="kpi-value">2</div><div class="kpi-subtext">7 sensors live</div></div>
            <div class="kpi-card"><div class="kpi-title">Active Assets</div><div class="kpi-value">9</div><div class="kpi-subtext">of 10 total</div></div>
            <div class="kpi-card"><div class="kpi-title">Low Stock Items</div><div class="kpi-value">4</div><div class="kpi-subtext">need reorder</div></div>
        </div>

        <div class="dashboard-grid">
            <div class="widget">
                <div class="widget-header">
                    <div class="widget-title"><i class="fa-solid fa-triangle-exclamation"></i> Critical / Overdue WOs</div>
                    <div class="widget-count-badge">2</div>
                </div>
                <div class="widget-body">
                    <div class="list-row"><div><div class="row-main-text">QC-01 SPREADER BEAM REPLACEMENT</div><div class="row-sub-text">Quay Crane QC-01</div></div><span class="status-tag tag-yellow">Due in 2d</span></div>
                    <div class="list-row"><div><div class="row-main-text"><i class="fa-solid fa-bolt" style="color: var(--badge-yellow);"></i> IoT Alert: DG-02 High Temp</div><div class="row-sub-text">Diesel Generator DG-02</div></div><span class="status-tag tag-yellow">Due in 0d</span></div>
                </div>
            </div>

            <div class="widget">
                <div class="widget-header purple-badge">
                    <div class="widget-title"><i class="fa-solid fa-tower-broadcast"></i> IoT Alerts</div>
                    <div class="widget-count-badge">2</div>
                </div>
                <div class="widget-body">
                    <div class="list-row"><div><div class="row-main-text">MP-01 Pump Monitor</div><div class="row-sub-text">Flow CRITICAL (328.9L/min &gt; 280L/min)</div></div><span class="status-tag tag-red">Alert</span></div>
                    <div class="list-row"><div><div class="row-main-text">AC-01 Compressor</div><div class="row-sub-text">Efficiency CRITICAL (94% &gt; 80%)</div></div><span class="status-tag tag-red">Alert</span></div>
                </div>
            </div>
        </div>

        <div class="dashboard-grid">
            <div class="widget">
                <div class="widget-header">
                    <div class="widget-title"><i class="fa-solid fa-business-time"></i> PM Due / Overdue</div>
                    <div class="widget-count-badge">4</div>
                </div>
                <div class="widget-body">
                    <div class="list-row"><div><div class="row-main-text">QC-01 — 250hr Service</div><div class="row-sub-text">250 hours • Auto</div></div><span class="status-tag tag-yellow">Due Soon</span></div>
                    <div class="list-row"><div><div class="row-main-text">DG-02 Monthly Check</div><div class="row-sub-text">Monthly • Auto</div></div><span class="status-tag tag-red">Overdue</span></div>
                    <div class="list-row"><div><div class="row-main-text">RTG-01 Weekly Greasing</div><div class="row-sub-text">Weekly • Auto</div></div><span class="status-tag tag-red">Overdue</span></div>
                </div>
            </div>

            <div class="widget">
                <div class="widget-header">
                    <div class="widget-title"><i class="fa-solid fa-boxes-stacked"></i> Low Stock Alerts</div>
                    <div class="widget-count-badge">4</div>
                </div>
                <div class="widget-body">
                    <div class="list-row"><div><div class="row-main-text">Spreader Twist Lock Assembly</div><div class="row-sub-text">SPR-TL-901 • 2/4 set</div></div><span class="status-tag tag-yellow">Low Stock</span></div>
                    <div class="list-row"><div><div class="row-main-text">Diesel Engine Oil 15W-40 (20L)</div><div class="row-sub-text">ENG-OIL-15W40 • 6/8 drum</div></div><span class="status-tag tag-yellow">Low Stock</span></div>
                    <div class="list-row"><div><div class="row-main-text">Oil Filter Cat 1R-0739</div><div class="row-sub-text">FILT-CAT-298739 • 4/6 ea</div></div><span class="status-tag tag-yellow">Low Stock</span></div>
                </div>
            </div>
        </div>
    </main>

    <main id="workorders-view" class="main-content">
        <div class="header">
            <h2>Work Orders</h2>
            <div class="live-indicator"><div class="live-dot"></div> LIVE</div>
        </div>

        <div class="action-bar">
            <div class="filter-tabs">
                <button class="tab-btn active">All</button>
                <button class="tab-btn">Open</button>
                <button class="tab-btn">In Progress</button>
                <button class="tab-btn">Completed</button>
                <button class="tab-btn">Cancelled</button>
            </div>
            <button class="btn-primary"><i class="fa-solid fa-plus"></i> New Work Order</button>
        </div>

        <div class="table-panel dark">
            <div class="table-panel-header">
                <div class="panel-title">Work Orders</div>
                <div class="search-container"><i class="fa-solid fa-magnifying-glass"></i><input type="text" placeholder="Search..."></div>
            </div>

            <table class="wo-table">
                <thead>
                    <tr>
                        <th>WO#</th><th>Title</th><th>Zone</th><th>Priority</th><th>Status</th><th>Assignee</th><th>Due</th><th>Actions</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td class="wo-id-cell"><div>WO1002</div><span class="auto-tag"><i class="fa-solid fa-bolt"></i> Auto</span></td>
                        <td><strong>DG-02 Oil &amp; Filter Change</strong><div class="title-subtext">Preventive</div></td>
                        <td>Power House</td>
                        <td><span class="status-tag tag-orange">High</span></td>
                        <td><span class="status-tag tag-pink">In Progress</span></td>
                        <td>James Thornton</td>
                        <td><span class="status-tag tag-yellow">Due in 2d</span></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-check"><i class="fa-solid fa-check"></i></button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell"><div>WO1003</div></td>
                        <td><strong>MP-01 Pump Seal Inspection</strong><div class="title-subtext">Inspection</div></td>
                        <td>Fuel Dock A</td>
                        <td><span class="status-tag tag-orange">High</span></td>
                        <td><span class="status-tag tag-muted-border">Open</span></td>
                        <td>Dimitri Vaskov</td>
                        <td><span class="status-tag tag-yellow">Due in 3d</span></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-check"><i class="fa-solid fa-check"></i></button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell"><div>WO1010</div><span class="auto-tag"><i class="fa-solid fa-bolt"></i> Auto</span></td>
                        <td><strong>[AUTO] DG-02 Monthly Check</strong><div class="title-subtext">Preventive</div></td>
                        <td>Power House</td>
                        <td><span class="status-tag tag-orange">High</span></td>
                        <td><span class="status-tag tag-muted-border">Open</span></td>
                        <td>James Thornton</td>
                        <td><span class="status-tag tag-red">Overdue 5d</span></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-check"><i class="fa-solid fa-check"></i></button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell"><div>WO1011</div><span class="auto-tag"><i class="fa-solid fa-bolt"></i> Auto</span></td>
                        <td><strong>[AUTO] RTG-01 Weekly Greasing</strong><div class="title-subtext">Preventive</div></td>
                        <td>Yard Zone A</td>
                        <td><span class="status-tag tag-orange">High</span></td>
                        <td><span class="status-tag tag-muted-border">Open</span></td>
                        <td>James Thornton</td>
                        <td><span class="status-tag tag-red">Overdue 1d</span></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-check"><i class="fa-solid fa-check"></i></button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell"><div>WO1084</div></td>
                        <td><strong>RTG-01 Wheel Bearing Replacement</strong><div class="title-subtext">Corrective</div></td>
                        <td>Yard Zone A</td>
                        <td><span class="status-tag tag-yellow">Medium</span></td>
                        <td><span class="status-tag tag-green">Completed</span></td>
                        <td>Marcus Chen</td>
                        <td><span class="status-tag tag-red">Overdue 5d</span></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell"><div>WO1089</div><span class="auto-tag"><i class="fa-solid fa-bolt"></i> Auto</span></td>
                        <td><strong>[AUTO] QC-01 — 250hr Service</strong><div class="title-subtext">Preventive</div></td>
                        <td>Berth 1</td>
                        <td><span class="status-tag tag-yellow">Medium</span></td>
                        <td><span class="status-tag tag-muted-border">Open</span></td>
                        <td>Marcus Chen</td>
                        <td><span class="status-tag tag-yellow">Due in 5d</span></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-check"><i class="fa-solid fa-check"></i></button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell"><div>WO1012</div><span class="auto-tag"><i class="fa-solid fa-bolt"></i> Auto</span></td>
                        <td><strong>[AUTO] SP-01 Annual Inspection</strong><div class="title-subtext">Preventive</div></td>
                        <td>Berth 3</td>
                        <td><span class="status-tag tag-yellow">Medium</span></td>
                        <td><span class="status-tag tag-muted-border">Open</span></td>
                        <td>Sarah O'Brien</td>
                        <td><span class="status-tag tag-yellow">Due in 0d</span></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-check"><i class="fa-solid fa-check"></i></button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </main>

    <main id="pm-view" class="main-content">
        <div class="header">
            <h2>Preventive Maintenance</h2>
            <div class="live-indicator"><div class="live-dot"></div> LIVE</div>
        </div>

        <div class="action-bar">
            <div class="filter-tabs">
                <button class="tab-btn active">All</button>
                <button class="tab-btn">Overdue</button>
                <button class="tab-btn">Due Soon</button>
                <button class="tab-btn">On Track</button>
            </div>
            <div class="right-actions">
                <button class="btn-secondary"><i class="fa-solid fa-bolt"></i> Auto-Schedule</button>
                <button class="btn-primary"><i class="fa-solid fa-plus"></i> New PM</button>
            </div>
        </div>

        <div class="table-panel light">
            <div class="table-panel-header">
                <div class="panel-title">Preventive Maintenance</div>
                <div class="search-container"><i class="fa-solid fa-magnifying-glass"></i><input type="text" placeholder="Search..."></div>
            </div>

            <table class="wo-table">
                <thead>
                    <tr>
                        <th>PM#</th><th>Schedule</th><th>Zone</th><th>Frequency</th><th>Last Done</th><th>Next Due</th><th>Status</th><th>Auto</th><th>Actions</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td class="wo-id-cell">PM1001</td>
                        <td><strong>QC-01 — 250hr Service</strong></td>
                        <td>Berth 1</td>
                        <td>250 Hours</td>
                        <td>27 Apr 2026</td>
                        <td>01 Jun 2026</td>
                        <td><span class="status-tag tag-yellow">Due Soon</span></td>
                        <td><span class="auto-tag"><i class="fa-solid fa-bolt"></i> Auto</span></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-check"><i class="fa-solid fa-check"></i></button>
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">PM1002</td>
                        <td><strong>DG-02 Monthly Check</strong></td>
                        <td>Power House</td>
                        <td>Monthly</td>
                        <td>22 Apr 2026</td>
                        <td>22 May 2026</td>
                        <td><span class="status-tag tag-red">Overdue</span></td>
                        <td><span class="auto-tag"><i class="fa-solid fa-bolt"></i> Auto</span></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-check"><i class="fa-solid fa-check"></i></button>
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">PM1003</td>
                        <td><strong>MP-01 Quarterly Inspection</strong></td>
                        <td>Fuel Dock A</td>
                        <td>Quarterly</td>
                        <td>28 Mar 2026</td>
                        <td>26 Jun 2026</td>
                        <td><span class="status-tag tag-green">On Track</span></td>
                        <td><span style="color:#5e3f3f;">Manual</span></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-check"><i class="fa-solid fa-check"></i></button>
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">PM1004</td>
                        <td><strong>RTG-01 Weekly Greasing</strong></td>
                        <td>Yard Zone A</td>
                        <td>Weekly</td>
                        <td>19 May 2026</td>
                        <td>26 May 2026</td>
                        <td><span class="status-tag tag-red">Overdue</span></td>
                        <td><span class="auto-tag"><i class="fa-solid fa-bolt"></i> Auto</span></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-check"><i class="fa-solid fa-check"></i></button>
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">PM1005</td>
                        <td><strong>SP-01 Annual Inspection</strong></td>
                        <td>Berth 3</td>
                        <td>Annually</td>
                        <td>27 May 2025</td>
                        <td>27 May 2025</td>
                        <td><span class="status-tag tag-yellow">Due Soon</span></td>
                        <td><span class="auto-tag"><i class="fa-solid fa-bolt"></i> Auto</span></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-check"><i class="fa-solid fa-check"></i></button>
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">PM1006</td>
                        <td><strong>QC-02 Wire Rope Lubrication</strong></td>
                        <td>Berth 2</td>
                        <td>Monthly</td>
                        <td>22 May 2026</td>
                        <td>21 Jun 2026</td>
                        <td><span class="status-tag tag-green">On Track</span></td>
                        <td><span style="color:#5e3f3f;">Manual</span></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-check"><i class="fa-solid fa-check"></i></button>
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">PM1007</td>
                        <td><strong>AC-01 Air Compressor Service</strong></td>
                        <td>Power House</td>
                        <td>Quarterly</td>
                        <td>12 May 2026</td>
                        <td>10 Aug 2026</td>
                        <td><span class="status-tag tag-green">On Track</span></td>
                        <td><span class="auto-tag"><i class="fa-solid fa-bolt"></i> Auto</span></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-check"><i class="fa-solid fa-check"></i></button>
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </main>

    <main id="assets-view" class="main-content">
        <div class="header">
            <h2>Port Assets</h2>
            <div class="live-indicator"><div class="live-dot"></div> LIVE</div>
        </div>

        <div class="action-bar">
            <div class="filter-tabs">
                <button class="tab-btn active">All</button>
                <button class="tab-btn">Active</button>
                <button class="tab-btn">Inactive</button>
                <button class="tab-btn">Decommissioned</button>
            </div>
            <button class="btn-primary"><i class="fa-solid fa-plus"></i> New Asset</button>
        </div>

        <div class="table-panel light">
            <div class="table-panel-header">
                <div class="panel-title">Port Assets</div>
                <div class="search-container"><i class="fa-solid fa-magnifying-glass"></i><input type="text" placeholder="Search..."></div>
            </div>

            <table class="wo-table">
                <thead>
                    <tr>
                        <th>ID</th><th>Name</th><th>Type</th><th>Zone</th><th>Criticality</th><th>Status</th><th>IoT</th><th>Last Maint.</th><th>Actions</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td class="wo-id-cell">ASS1001</td>
                        <td><strong>Quay Crane QC-01</strong><div class="title-subtext">Liebherr LHM 550</div></td>
                        <td>Crane</td>
                        <td>Berth 1</td>
                        <td><span class="status-tag tag-dark-red">Critical</span></td>
                        <td><span class="status-tag tag-light-gray">Active</span></td>
                        <td><span class="status-tag tag-yellow">Warn</span></td>
                        <td>07 May 2026</td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">ASS1002</td>
                        <td><strong>Quay Crane QC-02</strong><div class="title-subtext">Liebherr LHM 550</div></td>
                        <td>Crane</td>
                        <td>Berth 2</td>
                        <td><span class="status-tag tag-dark-red">Critical</span></td>
                        <td><span class="status-tag tag-light-gray">Active</span></td>
                        <td><span class="status-tag tag-light-gray">OK</span></td>
                        <td>12 May 2026</td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">ASS1003</td>
                        <td><strong>RTG Crane RTG-01</strong><div class="title-subtext">Kalmar RTG E-One</div></td>
                        <td>Crane</td>
                        <td>Yard Zone A</td>
                        <td><span class="status-tag tag-orange">High</span></td>
                        <td><span class="status-tag tag-light-gray">Active</span></td>
                        <td><span class="status-tag tag-yellow">Warn</span></td>
                        <td>22 May 2026</td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">ASS1004</td>
                        <td><strong>RTG Crane RTG-02</strong><div class="title-subtext">Kalmar RTG E-One</div></td>
                        <td>Crane</td>
                        <td>Yard Zone B</td>
                        <td><span class="status-tag tag-orange">High</span></td>
                        <td><span class="status-tag tag-light-gray" style="background-color:rgba(0,0,0,0.18);">Inactive</span></td>
                        <td><span class="status-tag tag-pink" style="background-color:var(--badge-purple)">Offline</span></td>
                        <td>27 Apr 2026</td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">ASS1005</td>
                        <td><strong>Reach Stacker RS-01</strong><div class="title-subtext">Hyster RS45-27CH</div></td>
                        <td>Mobile Equipment</td>
                        <td>Yard Zone A</td>
                        <td><span class="status-tag tag-yellow">Medium</span></td>
                        <td><span class="status-tag tag-light-gray">Active</span></td>
                        <td><span style="color:#5e3f3f;">No IoT</span></td>
                        <td>17 May 2026</td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">ASS1006</td>
                        <td><strong>Forklift FL-03</strong><div class="title-subtext">Toyota 8FBE20T</div></td>
                        <td>Mobile Equipment</td>
                        <td>Warehouse 1</td>
                        <td><span class="status-tag tag-green" style="background-color: #72b1b1;">Low</span></td>
                        <td><span class="status-tag tag-light-gray">Active</span></td>
                        <td><span style="color:#5e3f3f;">No IoT</span></td>
                        <td>19 May 2026</td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">ASS1007</td>
                        <td><strong>Marine Pump MP-01</strong><div class="title-subtext">Sulzer MPP-1500</div></td>
                        <td>Pump</td>
                        <td>Fuel Dock A</td>
                        <td><span class="status-tag tag-dark-red">Critical</span></td>
                        <td><span class="status-tag tag-light-gray">Active</span></td>
                        <td><span class="status-tag tag-red">Alert</span></td>
                        <td>12 Apr 2026</td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">ASS1008</td>
                        <td><strong>Diesel Generator DG-02</strong><div class="title-subtext">Caterpillar C3516</div></td>
                        <td>Generator</td>
                        <td>Power House</td>
                        <td><span class="status-tag tag-dark-red">Critical</span></td>
                        <td><span class="status-tag tag-light-gray">Active</span></td>
                        <td><span class="status-tag tag-red">Alert</span></td>
                        <td>22 Apr 2026</td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">ASS1009</td>
                        <td><strong>Shore Power SP-01</strong><div class="title-subtext">ABB AMPS-6000</div></td>
                        <td>Electrical</td>
                        <td>Berth 3</td>
                        <td><span class="status-tag tag-orange">High</span></td>
                        <td><span class="status-tag tag-light-gray">Active</span></td>
                        <td><span class="status-tag tag-yellow">Warn</span></td>
                        <td>07 May 2026</td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </main>

    <main id="iot-view" class="main-content">
        <div class="header">
            <h2>IoT Telemetry Hub</h2>
            <div class="live-indicator"><div class="live-dot"></div> LIVE</div>
        </div>

        <div class="action-bar">
            <div class="filter-tabs">
                <button class="tab-btn active">All Sensors</button>
                <button class="tab-btn"><i class="fa-solid fa-triangle-exclamation" style="color:#ff6b6b"></i> Alerts</button>
                <button class="tab-btn"><i class="fa-solid fa-circle-exclamation" style="color:#f1c40f"></i> Warnings</button>
                <button class="tab-btn">Normal</button>
                <button class="tab-btn">Offline</button>
            </div>
            <div class="right-actions">
                <button class="btn-secondary"><i class="fa-solid fa-rotate"></i> Refresh</button>
                <button class="btn-primary"><i class="fa-solid fa-plus"></i> Add Sensor</button>
            </div>
        </div>

        <div class="iot-grid">
            <div class="iot-card">
                <div class="iot-status-dot red"></div>
                <div class="iot-card-header">
                    <div class="iot-icon orange-bg"><i class="fa-solid fa-bolt"></i></div>
                    <div class="iot-card-title">
                        <h3>QC-01 Hoist Motor</h3>
                        <p>IOT1001 • Quay Crane QC-01</p>
                    </div>
                </div>
                <div class="iot-metrics-box">
                    <div class="metric-subcard"><div class="metric-label">Temp</div><div class="metric-val">82.0<span>°C</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Vibration</div><div class="metric-val">3.3<span>mm/s</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Current</div><div class="metric-val">104.5<span>A</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Runtime</div><div class="metric-val">12450.5</div></div>
                </div>
                <div class="iot-threshold-alert warning"><i class="fa-solid fa-triangle-exclamation"></i> temp approaching threshold (82°C/80°C)</div>
                <span class="iot-card-footer-time">Last: 27 May, 13:20</span>
            </div>

            <div class="iot-card">
                <div class="iot-status-dot green"></div>
                <div class="iot-card-header">
                    <div class="iot-icon orange-bg"><i class="fa-solid fa-bolt"></i></div>
                    <div class="iot-card-title">
                        <h3>QC-02 Main Drive</h3>
                        <p>IOT1002 • Quay Crane QC-02</p>
                    </div>
                </div>
                <div class="iot-metrics-box">
                    <div class="metric-subcard"><div class="metric-label">Temp</div><div class="metric-val">70.1<span>°C</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Vibration</div><div class="metric-val">-0.9<span>mm/s</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Current</div><div class="metric-val">85.9<span>A</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Runtime</div><div class="metric-val">9800.5</div></div>
                </div>
                <span class="iot-card-footer-time" style="margin-top: 48px; display: block;">Last: 27 May, 13:20</span>
            </div>

            <div class="iot-card">
                <div class="iot-status-dot red"></div>
                <div class="iot-card-header">
                    <div class="iot-icon orange-bg"><i class="fa-solid fa-bolt"></i></div>
                    <div class="iot-card-title">
                        <h3>RTG-01 Gantry Motor</h3>
                        <p>IOT1003 • RTG Crane RTG-01</p>
                    </div>
                </div>
                <div class="iot-metrics-box">
                    <div class="metric-subcard"><div class="metric-label">Temp</div><div class="metric-val">80.3<span>°C</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Vibration</div><div class="metric-val">1.7<span>mm/s</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Current</div><div class="metric-val">65.5<span>A</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Runtime</div><div class="metric-val">7200.5</div></div>
                </div>
                <div class="iot-threshold-alert warning"><i class="fa-solid fa-triangle-exclamation"></i> temp approaching threshold (80.3°C/80°C)</div>
                <span class="iot-card-footer-time">Last: 27 May, 13:20</span>
            </div>
        </div>

        <div class="iot-grid">
            <div class="iot-card">
                <div class="iot-status-dot red"></div>
                <div class="iot-card-header">
                    <div class="iot-icon orange-bg"><i class="fa-solid fa-bolt"></i></div>
                    <div class="iot-card-title">
                        <h3>RTG-02 Drive Motor</h3>
                        <p>IOT1004 • RTG Crane RTG-02</p>
                    </div>
                </div>
                <div class="iot-metrics-box">
                    <div class="metric-subcard"><div class="metric-label">Temp</div><div class="metric-val">0.0<span>°C</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Vibration</div><div class="metric-val">0.0<span>mm/s</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Current</div><div class="metric-val">0.0<span>A</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Runtime</div><div class="metric-val">5400.0</div></div>
                </div>
                <span class="iot-card-footer-time" style="margin-top: 48px; display: block;">Last: 27 May, 11:38</span>
            </div>

            <div class="iot-card">
                <div class="iot-status-dot green"></div>
                <div class="iot-card-header">
                    <div class="iot-icon blue-bg"><i class="fa-solid fa-droplet"></i></div>
                    <div class="iot-card-title">
                        <h3>MP-01 Pump Monitor</h3>
                        <p>IOT1005 • Marine Pump MP-01</p>
                    </div>
                </div>
                <div class="iot-metrics-box">
                    <div class="metric-subcard"><div class="metric-label">Pressure</div><div class="metric-val">6.3<span>BAR</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Flow</div><div class="metric-val">327.5<span>L/MIN</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Temp</div><div class="metric-val">48.5<span>°C</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Runtime</div><div class="metric-val">18000.0</div></div>
                </div>
                <div class="iot-threshold-alert" style="background:rgba(231,76,60,0.2); border-color:var(--badge-red); color:#ffcdd2;"><i class="fa-solid fa-triangle-exclamation"></i> flow CRITICAL (327.5L/min &gt; 200L/min)</div>
                <span class="iot-card-footer-time">Last: 27 May, 13:20</span>
            </div>

            <div class="iot-card">
                <div class="iot-status-dot green"></div>
                <div class="iot-card-header">
                    <div class="iot-icon green-bg"><i class="fa-solid fa-battery-three-quarters"></i></div>
                    <div class="iot-card-title">
                        <h3>DG-02 Engine Monitor</h3>
                        <p>IOT1006 • Diesel Generator DG-02</p>
                    </div>
                </div>
                <div class="iot-metrics-box">
                    <div class="metric-subcard"><div class="metric-label">Temp</div><div class="metric-val">113.2<span>°C</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Load</div><div class="metric-val">70.8<span>%</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Voltage</div><div class="metric-val">427.4<span>V</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Runtime</div><div class="metric-val">31000.0</div></div>
                </div>
                <div class="iot-threshold-alert" style="background:rgba(231,76,60,0.2); border-color:var(--badge-red); color:#ffcdd2;"><i class="fa-solid fa-triangle-exclamation"></i> temp CRITICAL (113.2°C &gt; 95°C)</div>
                <span class="iot-card-footer-time">Last: 27 May, 13:20</span>
            </div>
        </div>

        <div class="iot-grid">
            <div class="iot-card" style="grid-column: span 1;">
                <div class="iot-status-dot green"></div>
                <div class="iot-card-header">
                    <div class="iot-icon orange-bg" style="background: rgba(155, 89, 182, 0.2); color: var(--badge-purple);"><i class="fa-solid fa-bolt"></i></div>
                    <div class="iot-card-title">
                        <h3>SP-01 Power Panel</h3>
                        <p>IOT1007 • Shore Power SP-01</p>
                    </div>
                </div>
                <div class="iot-metrics-box">
                    <div class="metric-subcard"><div class="metric-label">Voltage</div><div class="metric-val">6586.6<span>V</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Current</div><div class="metric-val">55.3<span>A</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Power</div><div class="metric-val">364.2<span>KW</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Frequency</div><div class="metric-val">50.0<span>HZ</span></div></div>
                </div>
                <div class="iot-threshold-alert warning"><i class="fa-solid fa-triangle-exclamation"></i> power approaching threshold (364.2kW/350kW)</div>
                <span class="iot-card-footer-time">Last: 27 May, 13:21</span>
            </div>

            <div class="iot-card" style="grid-column: span 1;">
                <div class="iot-status-dot green"></div>
                <div class="iot-card-header">
                    <div class="iot-icon orange-bg" style="background: rgba(52, 152, 219, 0.2); color: #3498db;"><i class="fa-solid fa-compass"></i></div>
                    <div class="iot-card-title">
                        <h3>AC-01 Compressor</h3>
                        <p>IOT1008 • Air Compressor AC-01</p>
                    </div>
                </div>
                <div class="iot-metrics-box">
                    <div class="metric-subcard"><div class="metric-label">Pressure</div><div class="metric-val">9.5<span>BAR</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Temp</div><div class="metric-val">83.1<span>°C</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Runtime</div><div class="metric-val">4200.0<span>HRS</span></div></div>
                    <div class="metric-subcard"><div class="metric-label">Efficiency</div><div class="metric-val">94.0<span>%</span></div></div>
                </div>
                <div class="iot-threshold-alert" style="background:rgba(231,76,60,0.2); border-color:var(--badge-red); color:#ffcdd2;"><i class="fa-solid fa-triangle-exclamation"></i> temp CRITICAL (83.1°C &gt; 75°C)</div>
                <span class="iot-card-footer-time">Last: 27 May, 13:21</span>
            </div>
        </div>

        <div class="table-panel light">
            <div class="table-panel-header">
                <div class="panel-title">Sensor Log</div>
                <div class="search-container"><i class="fa-solid fa-magnifying-glass"></i><input type="text" placeholder="Filter logs..."></div>
            </div>
            <table class="wo-table">
                <thead>
                    <tr><th>Timestamp</th><th>Sensor</th><th>Status</th><th>Temp</th><th>Vibration / Pressure</th><th>Load / Flow</th></tr>
                </thead>
                <tbody>
                    <tr><td>27 May, 13:19</td><td>AC-01 Compressor</td><td><span class="status-tag tag-red">alert</span></td><td>82.6°</td><td>9.4 bar</td><td>—</td></tr>
                    <tr><td>27 May, 13:19</td><td>SP-01 Power Panel</td><td><span class="status-tag tag-yellow">warn</span></td><td>—</td><td>—</td><td>—</td></tr>
                    <tr><td>27 May, 13:19</td><td>DG-02 Engine Monitor</td><td><span class="status-tag tag-red">alert</span></td><td>113.2°</td><td>—</td><td>70%</td></tr>
                    <tr><td>27 May, 13:19</td><td>MP-01 Pump Monitor</td><td><span class="status-tag tag-red">alert</span></td><td>48.5°</td><td>6.4 bar</td><td>525 L/min</td></tr>
                </tbody>
            </table>
        </div>
    </main>

    <main id="map-view" class="main-content">
        <div class="header">
            <h2>Port Map & Zones</h2>
            <div class="live-indicator"><div class="live-dot"></div> LIVE</div>
        </div>

        <div class="action-bar">
            <div class="filter-tabs">
                <button class="tab-btn active">Port Map</button>
                <button class="tab-btn">Zone Management</button>
                <button class="tab-btn">Asset Tracking</button>
            </div>
        </div>

        <div class="map-container-panel">
            <div class="map-panel-header">
                <div class="panel-title">Port Facility Map</div>
                <div class="title-subtext" style="margin-top:0; color:var(--text-muted);">Click assets to view details - Pulsing = IoT Alert</div>
            </div>

            <div class="map-canvas">
                <div class="map-water-label">Harbor / Sea</div>
                <div class="map-grid-layout">
                    <div class="map-zone-block">Berth 1</div>
                    <div class="map-zone-block">Berth 2</div>
                    <div class="map-zone-block">Berth 3</div>
                </div>
                <div class="map-grid-layout">
                    <div class="map-zone-block yellow-zone">Yard Zone a</div>
                    <div class="map-zone-block yellow-zone">Yard Zone b</div>
                    <div class="map-zone-block purple-zone">Warehouse 1</div>
                </div>
                <div class="absolute-node powerhouse-node">Power House</div>
                <div class="absolute-node fueldock-node pulse-alert" style="border-color: var(--badge-red);">Fuel Dock A</div>
            </div>

            <div class="map-footer-legend">
                <div class="legend-items">
                    <div class="legend-item"><div class="legend-color" style="background-color: var(--badge-green);"></div> Normal</div>
                    <div class="legend-item"><div class="legend-color" style="background-color: var(--badge-yellow);"></div> Warning</div>
                    <div class="legend-item"><div class="legend-color" style="background-color: var(--badge-red);"></div> Alert (pulsing)</div>
                    <div class="legend-item"><div class="legend-color" style="background-color: var(--badge-blue);"></div> No IoT</div>
                </div>
                <div class="legend-meta" style="font-weight: 600; color: var(--text-muted);">10 assets plotted</div>
            </div>
        </div>
    </main>

    <main id="inventory-view" class="main-content">
        <div class="header">
            <h2>Parts &amp; Inventory</h2>
            <div class="live-indicator"><div class="live-dot"></div> LIVE</div>
        </div>

        <div class="action-bar">
            <div class="filter-tabs">
                <button class="tab-btn active">All Items</button>
                <button class="tab-btn">In Stock</button>
                <button class="tab-btn">Low Stock</button>
                <button class="tab-btn">On Order</button>
            </div>
            <button class="btn-primary"><i class="fa-solid fa-plus"></i> Add Part</button>
        </div>

        <div class="table-panel light">
            <div class="table-panel-header">
                <div class="panel-title">Parts Register</div>
                <div class="search-container"><i class="fa-solid fa-magnifying-glass"></i><input type="text" placeholder="Search inventory..."></div>
            </div>

            <table class="wo-table">
                <thead>
                    <tr>
                        <th>Part No.</th><th>Name</th><th>Zone</th><th>Qty</th><th>Min/Max</th><th>Unit Cost</th><th>Status</th><th>IoT</th><th>Actions</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td class="wo-id-cell">WR-32-STD</td>
                        <td><strong>Wire Rope 32mm (per meter)</strong><div class="title-subtext">Rigging • Industrial Parts Direct</div></td>
                        <td>Warehouse 1</td>
                        <td><strong>45 <span style="font-size: 11px; font-weight:400; color:#5e3f3f;">m</span></strong></td>
                        <td>20 / 200</td>
                        <td>$28.50</td>
                        <td><span class="status-tag tag-green">In Stock</span></td>
                        <td><span style="color:#5e3f3f;">—</span></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-qty"><i class="fa-solid fa-boxes-stacked"></i></button>
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">HYD-OIL-46</td>
                        <td><strong>Hydraulic Oil ISO VG46 (20L)</strong><div class="title-subtext">Lubricants • Industrial Parts Direct</div></td>
                        <td>Warehouse 1</td>
                        <td><strong>12 <span style="font-size:11px; font-weight:400; color:#5e3f3f;">drum</span></strong></td>
                        <td>10 / 60</td>
                        <td>$85.00</td>
                        <td><span class="status-tag tag-green">In Stock</span></td>
                        <td><span class="status-tag tag-pink" style="background-color: var(--badge-purple); font-size: 9px;">Tracked</span></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-qty"><i class="fa-solid fa-boxes-stacked"></i></button>
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">SPR-TL-091</td>
                        <td><strong>Spreader Twist Lock Assembly</strong><div class="title-subtext">Crane Parts • Liebherr Marine Cranes</div></td>
                        <td>Warehouse 1</td>
                        <td><strong>2 <span style="font-size:11px; font-weight:400; color:#5e3f3f;">set</span></strong></td>
                        <td>4 / 20</td>
                        <td>$6,250.00</td>
                        <td><span class="status-tag tag-yellow">Low Stock</span></td>
                        <td><span style="color:#5e3f3f;">—</span></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-qty"><i class="fa-solid fa-boxes-stacked"></i></button>
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">BRG-SKF-6320</td>
                        <td><strong>RTG Wheel Bearing SKF 6320</strong><div class="title-subtext">Bearings • Industrial Parts Direct</div></td>
                        <td>Warehouse 1</td>
                        <td><strong>8 <span style="font-size:11px; font-weight:400; color:#5e3f3f;">ea</span></strong></td>
                        <td>4 / 24</td>
                        <td>$145.00</td>
                        <td><span class="status-tag tag-green">In Stock</span></td>
                        <td><span style="color:#5e3f3f;">—</span></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-qty"><i class="fa-solid fa-boxes-stacked"></i></button>
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">ENG-OIL-15W40</td>
                        <td><strong>Diesel Engine Oil 15W-40 (20L)</strong><div class="title-subtext">Lubricants • Caterpillar Marine</div></td>
                        <td>Warehouse 1</td>
                        <td><strong>6 <span style="font-size:11px; font-weight:400; color:#5e3f3f;">drum</span></strong></td>
                        <td>8 / 49</td>
                        <td>$72.00</td>
                        <td><span class="status-tag tag-yellow">Low Stock</span></td>
                        <td><span class="status-tag tag-pink" style="background-color: var(--badge-purple); font-size: 9px;">Tracked</span></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-qty"><i class="fa-solid fa-boxes-stacked"></i></button>
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">SEAL-SZ-MP01</td>
                        <td><strong>Pump Mechanical Seal Kit</strong><div class="title-subtext">Pump Parts • Marine Hydraulics Pro</div></td>
                        <td>Warehouse 1</td>
                        <td><strong>3 <span style="font-size:11px; font-weight:400; color:#5e3f3f;">kit</span></strong></td>
                        <td>2 / 10</td>
                        <td>$680.00</td>
                        <td><span class="status-tag tag-green">In Stock</span></td>
                        <td><span style="color:#5e3f3f;">—</span></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-qty"><i class="fa-solid fa-boxes-stacked"></i></button>
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">CABLE-25SQ</td>
                        <td><strong>Electrical Cable 25mm² (per m)</strong><div class="title-subtext">Electrical • ABB Power</div></td>
                        <td>Warehouse 1</td>
                        <td><strong>150 <span style="font-size:11px; font-weight:400; color:#5e3f3f;">m</span></strong></td>
                        <td>50 / 500</td>
                        <td>$12.80</td>
                        <td><span class="status-tag tag-green">In Stock</span></td>
                        <td><span style="color:#5e3f3f;">—</span></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-qty"><i class="fa-solid fa-boxes-stacked"></i></button>
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </main>

    <main id="technicians-view" class="main-content">
        <div class="header">
            <h2>Technicians Directory</h2>
            <div class="live-indicator"><div class="live-dot"></div> LIVE</div>
        </div>

        <div class="action-bar">
            <div class="filter-tabs">
                <button class="tab-btn active">All Staff</button>
                <button class="tab-btn">Active Now</button>
                <button class="tab-btn">On Leave</button>
            </div>
            <button class="btn-primary"><i class="fa-solid fa-user-plus"></i> Add Technician</button>
        </div>

        <div class="table-panel dark">
            <div class="table-panel-header">
                <div class="panel-title">Engineering Personnel</div>
                <div class="search-container"><i class="fa-solid fa-magnifying-glass"></i><input type="text" placeholder="Search engineers..."></div>
            </div>

            <table class="wo-table">
                <thead>
                    <tr>
                        <th>ID</th><th>Name &amp; Contacts</th><th>Operational Role</th><th>Specialty Discipline</th><th>Assigned Zone</th><th>Status</th><th>Open WOs</th><th>Actions</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td class="wo-id-cell">TEC1001</td>
                        <td><strong>Marcus Chen</strong><span class="sub-email">m.chen@port.com</span></td>
                        <td>Senior Mechanical Engineer</td>
                        <td>Cranes &amp; Heavy Equipment</td>
                        <td>Berth 1</td>
                        <td><span class="status-tag tag-green">Active</span></td>
                        <td><div class="wo-count-box" style="color: #ff6b6b;">7</div></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">TEC1002</td>
                        <td><strong>Sarah O'Brien</strong><span class="sub-email">s.obrien@port.com</span></td>
                        <td>Electrical Technician</td>
                        <td>Power Systems &amp; Controls</td>
                        <td>Power House</td>
                        <td><span class="status-tag tag-green">Active</span></td>
                        <td><div class="wo-count-box" style="color: var(--badge-yellow);">1</div></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">TEC1003</td>
                        <td><strong>Dimitri Vaskov</strong><span class="sub-email">d.vaskov@port.com</span></td>
                        <td>Hydraulic Specialist</td>
                        <td>Hydraulics &amp; Pneumatics</td>
                        <td>Fuel Dock A</td>
                        <td><span class="status-tag tag-green">Active</span></td>
                        <td><div class="wo-count-box" style="color: var(--badge-yellow);">1</div></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">TEC1004</td>
                        <td><strong>Angela Reyes</strong><span class="sub-email">a.reyes@port.com</span></td>
                        <td>Mechanical Technician</td>
                        <td>Pumps &amp; Pipelines</td>
                        <td>Berth 2</td>
                        <td><span class="status-tag tag-green">Active</span></td>
                        <td><div class="wo-count-box" style="color: var(--text-muted);">0</div></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">TEC1B05</td>
                        <td><strong>James Thornton</strong><span class="sub-email">j.thornton@port.com</span></td>
                        <td>Lead Technician</td>
                        <td>General Maintenance</td>
                        <td>Yard Zone A</td>
                        <td><span class="status-tag tag-green">Active</span></td>
                        <td><div class="wo-count-box" style="color: #ff6b6b;">4</div></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">TEC1006</td>
                        <td><strong>Priya Nair</strong><span class="sub-email">p.nair@port.com</span></td>
                        <td>Instrumentation Tech</td>
                        <td>Sensors &amp; SCADA</td>
                        <td>Power House</td>
                        <td><span class="status-tag tag-black">Inactive</span></td>
                        <td><div class="wo-count-box" style="color: var(--text-muted);">0</div></td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </main>

    <main id="vendors-view" class="main-content">
        <div class="header">
            <h2>Vendors &amp; Contractors</h2>
            <div class="live-indicator"><div class="live-dot"></div> LIVE</div>
        </div>

        <div class="action-bar">
            <div class="filter-tabs">
                <button class="tab-btn active">All External Partners</button>
                <button class="tab-btn">OEMs</button>
                <button class="tab-btn">Contracted Service</button>
            </div>
            <button class="btn-primary"><i class="fa-solid fa-plus"></i> Add Vendor</button>
        </div>

        <div class="table-panel light-dark-mix">
            <div class="table-panel-header">
                <div class="panel-title">Corporate Vendors &amp; Suppliers</div>
                <div class="search-container"><i class="fa-solid fa-magnifying-glass"></i><input type="text" placeholder="Search suppliers..."></div>
            </div>

            <table class="wo-table">
                <thead>
                    <tr>
                        <th>ID</th><th>Name</th><th>Category</th><th>Primary Contact</th><th>Contract Expiry</th><th>Rating</th><th>Actions</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td class="wo-id-cell">VEN1001</td>
                        <td><strong>Liebherr Marine Cranes</strong></td>
                        <td>Crane OEM</td>
                        <td>Karl Weber<span class="sub-email">k.weber@liebherr.com</span></td>
                        <td><span class="status-tag tag-muted-border">Due 27 May 2027</span></td>
                        <td>
                            <div class="stars-container">
                                <i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i>
                            </div>
                        </td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">VEN1002</td>
                        <td><strong>Kalmar Global</strong></td>
                        <td>Crane OEM</td>
                        <td>Lisa Chang<span class="sub-email">l.chang@kalmar.com</span></td>
                        <td><span class="status-tag tag-muted-border">Due 13 Dec 2026</span></td>
                        <td>
                            <div class="stars-container">
                                <i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i>
                            </div>
                        </td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">VEN1003</td>
                        <td><strong>Marine Hydraulics Pro</strong></td>
                        <td>Hydraulics</td>
                        <td>Bob Steelman<span class="sub-email">b.steelman@mhp.com</span></td>
                        <td><span class="status-tag tag-muted-border">Due 16 Jul 2026</span></td>
                        <td>
                            <div class="stars-container">
                                <i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i>
                            </div>
                        </td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">VEN1084</td>
                        <td><strong>ABB Power Solutions</strong></td>
                        <td>Electrical</td>
                        <td>Elena Kovic<span class="sub-email">e.kovic@abb.com</span></td>
                        <td><span class="status-tag tag-muted-border">Due 19 Sept 2027</span></td>
                        <td>
                            <div class="stars-container">
                                <i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i>
                            </div>
                        </td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">VEN1005</td>
                        <td><strong>Industrial Parts Direct</strong></td>
                        <td>Parts Supplier</td>
                        <td>Mike Santos<span class="sub-email">m.santos@ipd.com</span></td>
                        <td><span class="status-tag tag-muted-border">Due 25 Aug 2026</span></td>
                        <td>
                            <div class="stars-container">
                                <i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i>
                            </div>
                        </td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td class="wo-id-cell">VEN1086</td>
                        <td><strong>Caterpillar Marine</strong></td>
                        <td>Generator OEM</td>
                        <td>Tom Harris<span class="sub-email">t.harris@cat.com</span></td>
                        <td><span class="status-tag tag-muted-border">Due 13 Dec 2026</span></td>
                        <td>
                            <div class="stars-container">
                                <i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i>
                            </div>
                        </td>
                        <td>
                            <div class="action-buttons">
                                <button class="btn-action btn-edit">Edit</button>
                                <button class="btn-action btn-delete"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </main>

    <script>
        function switchView(viewId, element) {
            // Content panel router
            document.querySelectorAll('.main-content').forEach(view => {
                view.classList.remove('active-view');
            });
            document.getElementById(viewId).classList.add('active-view');

            // Sidebar navigation state router
            document.querySelectorAll('.menu-item').forEach(item => {
                item.classList.remove('active');
            });
            element.classList.add('active');
        }
    </script>
</body>
</html>
