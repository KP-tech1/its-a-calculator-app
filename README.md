<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WorkRightTT - Find Your Perfect Job in Trinidad and Tobago</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css">
    <style>
 :root {
            --primary-blue: #0066cc;
            --secondary-blue: #004d99;
            --accent-yellow: #ffcc00;
            --accent-red: #cc0000;
            --light-gray: #f5f5f5;
            --dark-gray: #333333;
            --white: #ffffff;
            --primary: #cc0000;
            --secondary: #f0f0f0;
\
            --accent: #ffcc00;
            --text: #333333;
            --light: #ffffff;
            --dark: #000000;
            --success: #28a745;
            --info: #17a2b8;
            --warning: #ffc107;
            --danger: #dc3545;
            --purple: #6f42c1;
            --pink: #e83e8c;
            --teal: #20c997;
        }
        
        /* Dark mode variables */
   :root.dark-mode {
    --primary-blue: #3399ff;
    --secondary-blue: #66b3ff;
    --accent-yellow: #A0522D; 
    --accent-red: #ff3333;
    --light-gray: #121212; 
    --dark-gray: #e6e6e6;
    --white: #0a0a0a; 
    --secondary: #1e1e1e; 
    --text: #e6e6e6;
    --light: #0a0a0a;
    --reset-btn-color: #555; 
}

/* Reset search button in dark mode */
:root.dark-mode #reset-search-btn {
    background-color: var(--reset-btn-color) !important;
}
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            transition: background-color 0.3s, color 0.3s;
        }
        
        body {
    background-color: var(--light-gray);
    color: var(--dark-gray);
    line-height: 1.6;
    padding-top: 80px; /* For fixed header on desktop */
}

@media (max-width: 768px) {
    body {
        padding-top: 60px; /* Smaller padding for mobile header */
    }
}

        /* High contrast mode */
        :root.high-contrast {
            --primary-blue: #0000FF;
            --secondary-blue: #0000A0;
            --accent-yellow: #FFFF00;
            --accent-red: #FF0000;
            --light-gray: #FFFFFF;
            --dark-gray: #000000;
            --white: #FFFFFF;
            --secondary: #EEEEEE;
            --text: #000000;
            --light: #FFFFFF;
        }
        
        /* Low contrast mode */
        :root.low-contrast {
            --primary-blue: #7A9CC6;
            --secondary-blue: #5A7BA6;
            --accent-yellow: #E6C229;
            --accent-red: #C75D5D;
            --light-gray: #F0F0F0;
            --dark-gray: #555555;
            --white: #F5F5F5;
            --secondary: #E0E0E0;
            --text: #555555;
            --light: #F5F5F5;
        }
        
        /* Dark mode toggle button */
        .dark-mode-toggle {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background-color: var(--primary-blue);
            color: white;
            border: none;
            border-radius: 50%;
            width: 50px;
            height: 50px;
            font-size: 1.5rem;
            cursor: pointer;
            z-index: 1000;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        .dark-mode-toggle:hover {
            background-color: var(--secondary-blue);
        }
        
      
/* Job Details Modal */
.job-details-modal {
    display: none;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.7);
    z-index: 1001;
    justify-content: center;
    align-items: center;
    padding: 20px;
    box-sizing: border-box;
}

.job-details-modal.active {
    display: flex;
}

.job-details-content {
    background-color: var(--white);
    border-radius: 12px;
    padding: 2rem;
    width: 100%;
    max-width: 800px;
    max-height: 90vh;
    overflow-y: auto;
    position: relative;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
}

.job-details-close {
    position: absolute;
    top: 15px;
    right: 15px;
    background: none;
    border: none;
    font-size: 1.5rem;
    cursor: pointer;
    color: #777;
}

.job-details-header {
    margin-bottom: 1.5rem;
    padding-bottom: 1rem;
    border-bottom: 1px solid #eee;
}

.job-details-header h2 {
    color: var(--primary-blue);
    margin-bottom: 0.5rem;
    font-size: 1.8rem;
}

.job-meta-row {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
    margin-bottom: 0.5rem;
    color: #666;
    font-size: 0.95rem;
}

.job-meta-item {
    display: flex;
    align-items: center;
    gap: 5px;
}

.job-details-section {
    margin-bottom: 1.5rem;
}

.job-details-section h3 {
    color: var(--primary-blue);
    margin-bottom: 0.8rem;
    font-size: 1.3rem;
}

.job-details-section p, 
.job-details-section ul {
    margin-bottom: 1rem;
    line-height: 1.6;
}

.job-details-section ul {
    padding-left: 1.5rem;
}

.job-details-urgent {
    display: inline-block;
    background-color: var(--accent-red);
    color: white;
    padding: 3px 10px;
    border-radius: 3px;
    font-size: 0.8rem;
    font-weight: bold;
    margin-left: 10px;
}

.job-details-company {
    background-color: var(--light-gray);
    padding: 1.5rem;
    border-radius: 8px;
    margin-top: 2rem;
}

.job-details-company h3 {
    color: var(--primary-blue);
    margin-bottom: 1rem;
}

.view-details-btn {
    position: absolute;
    top: 40px; /* Changed from relative to absolute and increased top value */
    right: 15px;
    background: none;
    border: none;
    color: var(--primary-blue);
    font-size: 1.2rem;
    cursor: pointer;
    transition: color 0.3s;
    padding: 0;
    display: block;
}

.view-details-btn:hover {
    color: var(--secondary-blue);
}

.social-share {
    display: flex;
    align-items: center;
    padding: 8px 0;
    border-top: 1px solid #eee;
    border-bottom: 1px solid #eee;
    margin-bottom: 15px;
}

.social-share a {
    font-size: 1.2rem;
    text-decoration: none;
    transition: transform 0.2s;
}

.social-share a:hover {
    transform: translateY(-2px);
}


/* Responsive adjustments */
@media (max-width: 768px) {
    .job-details-content {
        padding: 1.5rem;
    }
    
    .job-details-header h2 {
        font-size: 1.5rem;
    }
    
    .view-details-btn {
        right: 45px;
        font-size: 1.1rem;
    }
}

@media (max-width: 480px) {
    .job-details-content {
        padding: 1rem;
    }
    
    .job-meta-row {
        flex-direction: column;
        gap: 0.5rem;
    }
    
    .view-details-btn {
        right: 40px;
        font-size: 1rem;
    }
}

/* Grid Style Options */
.grid-style-container {
    margin: 0.5rem 0;
    display: flex;
    align-items: center;
    gap: 5px;
    font-size: 0.85rem;
}

.grid-style-container span {
    font-weight: 500;
    margin-right: 5px;
}

.grid-style-btn {
    padding: 5px 8px;
    background-color: var(--light-gray);
    color: var(--dark-gray);
    border: 1px solid #ddd;
    border-radius: 4px;
    font-size: 0.8rem;
    min-width: 30px;
}

.grid-style-btn i {
    font-size: 0.9rem;
}

.grid-style-btn.active {
    background-color: var(--primary-blue);
    color: white;
    border-color: var(--primary-blue);
}

.grid-style-btn:hover {
    background-color: #e0e0e0;
}

/* Grid View (default) */
.jobs-container.grid-view {
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 2rem;
}

/* List View */
.jobs-container.list-view {
    grid-template-columns: 1fr;
    gap: 1rem;
}

.jobs-container.list-view .job-card {
    flex-direction: row;
    align-items: flex-start;
    padding: 1.5rem;
}

.jobs-container.list-view .job-card > * {
    flex: 1;
    margin-bottom: 0;
}

.jobs-container.list-view .job-card .job-actions {
    flex-direction: column;
    align-items: flex-end;
    justify-content: center;
}

.jobs-container.list-view .job-card .job-meta {
    flex-direction: column;
    gap: 5px;
}
.jobs-container.list-view .job-card h3 {
    margin-right: 1.0rem; 
    min-width: 200px; 
}

/* Compact View */
.jobs-container.compact-view {
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 1rem;
}

.jobs-container.compact-view .job-card {
    padding: 1rem;
}

.jobs-container.compact-view .job-card h3 {
    font-size: 1.1rem;
}

.jobs-container.compact-view .job-card .description,
.jobs-container.compact-view .job-card .requirements {
    display: none;
}

.jobs-container.compact-view .job-card .job-actions {
    margin-top: 0.5rem;
}


        /* Logo Styles */
        .logo {
            display: flex;
            align-items: center;
            transition: all 0.3s ease;
        }
        
        .logo-img {
            height: 60px;
            margin-right: 10px;
            transition: all 0.3s ease;
            font-size: 2.5rem;
        }
        
        .logo-text {
            display: flex;
            flex-direction: column;
        }
        
        .logo-main {
            font-size: 1.8rem;
            font-weight: 700;
            color: var(--white);
            line-height: 1;
            transition: all 0.3s ease;
        }
        
        .logo-sub {
            font-size: 0.7rem;
            color: var(--accent-yellow);
            letter-spacing: 1px;
            transition: all 0.3s ease;
        }
        
        .logo span {
            color: var(--accent-yellow);
        }
        
        /* Fixed Header */
        header {
            background: linear-gradient(135deg, var(--primary-blue), var(--secondary-blue));
            color: var(--white);
            padding: 0.5rem 0;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
            transition: all 0.3s ease;
        }

@media (max-width: 768px) {
    body {
        padding-top: 70px; /* Increased padding for mobile header */
    }
    
    header {
        padding: 0.5rem 0; /* Slightly more padding */
        height: 70px; /* Fixed height for mobile header */
    }

    .header-content {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 0 10px;
        flex-wrap: nowrap;
    }
    
    .logo {
        display: flex;
        align-items: center;
        flex-shrink: 0;
        order: 1; /* Logo on the left */
        max-width: 60%;
    }
    
    .logo-img {
        height: 40px !important;
        margin-right: 5px;
    }
    
    .logo-text {
        margin-left: 0;
        flex-shrink: 1;
        overflow: hidden;
    }
    
    .logo-main {
        font-size: 1.3rem !important;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
    }
    
    .logo-sub {
        font-size: 0.5rem !important;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
    }
    .logo.home-link {
    text-decoration: none;
    display: flex;
    align-items: center;
    transition: all 0.3s ease;
    color: inherit;
}

    /* Mobile menu button styling */
    .mobile-menu-btn {
        font-size: 1.8rem;
        padding: 5px;
        background: rgba(255,255,255,0.1);
        border-radius: 5px;
        order: 3; /* Menu button on the far right */
        margin-left: 10px;
        flex-shrink: 0;
    }
    
    /* Navigation menu container */
    nav {
        order: 2; /* Navigation in the middle (though it will be hidden) */
        margin-left: auto;
    }
    
    /* Improved mobile menu dropdown */
    nav ul {
        display: none;
        position: absolute;
        top: 100%;
        right: 0;
        width: 200px;
        background: var(--secondary-blue);
        margin-top: 0;
        padding: 10px 0;
        max-height: calc(100vh - 60px);
        overflow-y: auto;
        box-shadow: -2px 2px 5px rgba(0,0,0,0.2);
    }
    
    nav ul.show {
        display: block;
    }
    
    nav ul li {
        width: 100%;
        text-align: left;
    }
    
    nav ul li a {
        padding: 10px 15px;
        justify-content: flex-start;
    }
    
    /* Adjust hero section for mobile */
    .hero {
        height: 300px;
        margin-top: 0;
    }
    
    .hero-content {
        padding: 20px;
    }
    
    .hero h2 {
        font-size: 1.8rem;
    }
    
    .hero p {
        font-size: 1rem;
    }
}        
        .header-scrolled {
            padding: 0.2rem 0;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
        }
        
        .header-scrolled .logo-img {
            height: 50px;
        }
        
        .header-scrolled .logo-main {
            font-size: 1.5rem;
        }
        
        .header-scrolled .logo-sub {
            font-size: 0.6rem;
        }
        
        .container {
            width: 90%;
            max-width: 1200px;
            margin: 0 auto;
        }
        
        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        nav ul {
            display: flex;
            list-style: none;
        }
        
        nav ul li {
            margin-left: 1.5rem;
            position: relative;
        }
        
        nav ul li a {
            color: var(--white);
            text-decoration: none;
            font-weight: 500;
            transition: color 0.3s;
            padding: 0.5rem 0;
            border-bottom: 2px solid transparent;
            display: flex;
            align-items: center;
        }
        
        nav ul li a i {
            margin-right: 5px;
        }
        
        nav ul li a:hover, nav ul li a.active {
            color: var(--accent-yellow);
            border-bottom: 2px solid var(--accent-yellow);
        }
        
        /* Dropdown menu styles */
        .dropdown {
            position: relative;
        }
        
        .dropdown-content {
            display: none;
            position: absolute;
            background-color: var(--secondary-blue);
            min-width: 200px;
            box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
            z-index: 1;
            border-radius: 0 0 5px 5px;
            top: 100%;
            left: 0;
        }
        
        .dropdown-content a {
            color: var(--white);
            padding: 12px 16px;
            text-decoration: none;
            display: block;
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }
        
        .dropdown-content a:hover {
            background-color: var(--primary-blue);
        }
        
        .dropdown:hover .dropdown-content {
            display: block;
        }
        
        .dropdown:hover .dropbtn {
            color: var(--accent-yellow);
            border-bottom: 2px solid var(--accent-yellow);
        }
        
        .mobile-menu-btn {
            display: none;
            background: none;
            border: none;
            color: var(--white);
            font-size: 1.5rem;
            cursor: pointer;
        }
        
        /* Hero Section */
       .hero {
    background: url('https://images.unsplash.com/photo-1521791136064-7986c2920216?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80') no-repeat center center/cover;
    height: 500px;
    display: flex;
    align-items: center;
    position: relative;
    z-index: 1;
    margin-top: -80px;
}

@media (max-width: 768px) {
    .hero {
        height: 400px;
        margin-top: -70px; /* Match the header height */
        padding-top: 70px; /* Push content down below header */
    }
    
    .hero-content {
        padding-top: 40px; /* Additional spacing for content */
    }
}
        
        .hero::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
        }
        
        .hero-content {
    position: relative;
    z-index: 1;
    color: var(--white);
    max-width: 600px;
    margin-top: 20px; /* Push content down */
}

@media (max-width: 768px) {
    .hero-content {
        margin-top: 40px; /* More space on mobile */
        padding: 0 20px; /* Side padding */
    }
}
        
        .hero h2 {
            font-size: 2.5rem;
            margin-bottom: 1rem;
            line-height: 1.2;
        }
        
        .hero p {
            font-size: 1.2rem;
            margin-bottom: 2rem;
        }
        
        .btn {
            display: inline-block;
            background-color: var(--accent-yellow);
            color: var(--dark-gray);
            padding: 0.8rem 1.5rem;
            border-radius: 5px;
            text-decoration: none;
            font-weight: 600;
            transition: all 0.3s;
            border: none;
            cursor: pointer;
            text-align: center;
        }
        
        .btn:hover {
            background-color: #e6b800;
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        
        .btn-blue {
            background-color: var(--primary-blue);
            color: white;
        }
        
        .btn-blue:hover {
            background-color: var(--secondary-blue);
        }
        
        .btn-red {
            background-color: var(--accent-red);
            color: white;
        }
        
        .btn-red:hover {
            background-color: #b30000;
        }
        
        /* Features Section */
        .features {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 2rem;
            margin: 3rem 0;
        }
        
        .feature-card {
            background-color: var(--white);
            border-radius: 8px;
            padding: 1.5rem;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            transition: all 0.3s;
            text-align: center;
            border: 1px solid #eee;
        }
        
        .feature-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
        }
        
        .feature-card i {
            font-size: 2.5rem;
            color: var(--primary-blue);
            margin-bottom: 1rem;
            background: linear-gradient(135deg, var(--primary-blue), var(--secondary-blue));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .feature-card h3 {
            margin-bottom: 1rem;
            color: var(--primary-blue);
        }
        
        /* Section Titles */
        .section-title {
            text-align: center;
            margin: 3rem 0;
            color: var(--primary-blue);
        }
        
        .section-title h2 {
            font-size: 2rem;
            margin-bottom: 1rem;
            position: relative;
            display: inline-block;
        }
        
        .section-title h2::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 80px;
            height: 3px;
            background: var(--accent-yellow);
        }
        
        .section-title p {
            max-width: 700px;
            margin: 0 auto;
        }

/* Floating Controls Container */
.floating-controls-container {
    position: fixed;
    bottom: 20px;
    right: 20px;
    z-index: 1000;
    display: flex;
    flex-direction: column-reverse;
    align-items: flex-end;
    gap: 15px;
}

.floating-controls-main-toggle {
    background-color: var(--primary-blue);
    color: white;
    border: none;
    border-radius: 50%;
    width: 50px;
    height: 50px;
    font-size: 1.5rem;
    cursor: pointer;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
    display: flex;
    justify-content: center;
    align-items: center;
    transition: all 0.3s ease;
    z-index: 1001;
}

.floating-controls-main-toggle:hover {
    background-color: var(--secondary-blue);
    transform: rotate(45deg);
}

.floating-controls-buttons {
    display: flex;
    flex-direction: column;
    gap: 15px;
    opacity: 0;
    visibility: hidden;
    transform: translateY(20px);
    transition: all 0.3s ease;
}

.floating-controls-container.expanded .floating-controls-buttons {
    opacity: 1;
    visibility: visible;
    transform: translateY(0);
}

/* Adjust existing toggle positions */
.accessibility-toggle, 
.language-toggle, 
.dark-mode-toggle {
    position: static;
    bottom: auto;
    right: auto;
    margin: 0;
}


/* Filter Toggle Styles */
.filter-toggle-container {
    text-align: center;
    margin: 15px 0;
}

.filter-toggle-container .btn {
    background-color: var(--primary-blue);
    color: white;
    padding: 8px 20px;
    border-radius: 20px;
    font-size: 0.9rem;
    transition: all 0.3s;
}

.filter-toggle-container .btn:hover {
    background-color: var(--secondary-blue);
    transform: translateY(-2px);
}

.filter-toggle-container .btn i {
    margin-right: 5px;
}

.advanced-filters-container {
    background-color: var(--white);
    padding: 15px;
    border-radius: 8px;
    margin: 10px 0;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

/* Responsive adjustments */
@media (max-width: 768px) {
    .filter-toggle-container .btn {
        width: 100%;
        padding: 10px;
    }
    
    .advanced-filters-container {
        padding: 10px;
    }
}

@media (max-width: 768px) {
    .filter-toggle-container#location-toggle-container {
        width: 100%;
        max-width: 100%;
    }
    
    #toggle-location-filters-btn {
        width: 100%;
        padding: 8px !important;
    }
}
        
        /* Jobs Section */
        .jobs-section {
            padding: 3rem 0;
            background-color: var(--white);
        }
        
        .jobs-filters {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-bottom: 20px;
        }
        
        .filter-group {
            flex: 1;
            min-width: 200px;
        }
        
        .filter-group select {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
        
        .jobs-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 2rem;
        }
        
        .job-card {
            background-color: var(--light-gray);
            border-radius: 8px;
            padding: 1.5rem;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
            transition: all 0.3s;
            border: 1px solid #eee;
            display: flex;
            flex-direction: column;
            position: relative;
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
        }
        
        .job-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
        }
        
        .job-card h3 {
    color: var(--primary-blue);
    margin-bottom: 0.5rem;
    font-size: 1.25rem;
    font-weight: 600;
    line-height: 1.3;
}
        
        .job-card .company {
    font-weight: 600;
    margin-bottom: 0.5rem;
    color: var(--secondary-blue);
    cursor: pointer;
    display: inline-block;
    font-size: 1rem;
}
        
        .job-card .company:hover {
            text-decoration: underline;
        }
        
        .job-card .location {
            display: flex;
            align-items: center;
            margin-bottom: 0.5rem;
            color: #666;
            cursor: pointer;
        }
        
        .job-card .location:hover {
            text-decoration: underline;
        }
        
        .job-card .location i {
            margin-right: 5px;
        }
        
        .job-card .salary {
            font-weight: 600;
            margin-bottom: 1rem;
            color: var(--accent-red);
        }

.job-card .salary.undisclosed {
    color: #666;
    font-style: italic;
    font-weight: normal;
}
        
        .job-card .description {
    margin-bottom: 1.5rem;
    flex-grow: 1;
    font-size: 0.95rem;
    line-height: 1.5;
    color: var(--dark-gray);
}
        
        .job-card .job-meta {
    display: flex;
    justify-content: space-between;
    margin-bottom: 1rem;
    font-size: 0.85rem;
    color: #666;
}

.job-card .deadline {
    font-size: 0.85rem;
    color: var(--accent-red);
    margin-bottom: 0.5rem;
    font-weight: 500;
}
        
        .job-card .job-actions {
            display: flex;
            gap: 10px;
        }
        
        .job-card .btn {
            flex: 1;
            text-align: center;
        }
        
.job-card .requirements {
    margin-bottom: 1rem;
    color: var(--dark-gray);
    font-size: 0.9rem;
    line-height: 1.5;
    font-weight: 400;
}

.urgent-badge {
    display: inline-block;
    background-color: var(--accent-red);
    color: white;
    padding: 2px 6px;
    border-radius: 10px;
    font-size: 0.7rem;
    font-weight: bold;
    margin-left: 8px;
    text-transform: uppercase;
    line-height: 1.2;
}

        /* Verified badge */
        .verified-badge {
            position: absolute;
            top: 15px;
            right: 15px;
            color: var(--primary-blue);
            font-size: 1.2rem;
            display: none;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .verified-badge::after {
    content: 'Verified by WorkrightTT';
    position: absolute;
    right: 100%;
    top: 50%;
    transform: translateY(-50%);
    background-color: var(--primary-blue);
    color: white;
    padding: 10px 15px;
    border-radius: 6px;
    font-size: 0.9rem;
    width: max-content;
    max-width: 200px;
    opacity: 0;
    transition: opacity 0.3s, transform 0.2s;
    pointer-events: none;
    margin-right: 10px;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-weight: 500;
    letter-spacing: 0.5px;
    box-shadow: 0 3px 8px rgba(0,0,0,0.2);
    transform-origin: right center;
}
        
        .verified-badge:hover::after {
            opacity: 1;
            transform: translateY(-50%) scale(1);
        }
        
        .job-card.verified .verified-badge {
            display: block;
        }

        /* Company verified badge */
        .company-verified {
            display: inline-block;
            color: var(--primary-blue);
            font-size: 0.8rem;
            margin-left: 5px;
            cursor: pointer;
        }
        
.company-verified::after {
    content: 'Company Verified by WorkrightTT';
    position: absolute;
    background-color: var(--primary-blue);
    color: white;
    padding: 10px 15px;
    border-radius: 6px;
    font-size: 0.9rem;
    width: max-content;
    max-width: 220px;
    opacity: 0;
    transition: opacity 0.3s;
    pointer-events: none;
    margin-top: 15px;
    margin-left: -110px;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-weight: 500;
    letter-spacing: 0.5px;
    box-shadow: 0 3px 8px rgba(0,0,0,0.2);
}
        
        .company-verified:hover::after {
            opacity: 1;
        }

        /* Pinned job indicator */
        .pinned-badge {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            background-color: var(--accent-yellow);
            color: var(--dark-gray);
            padding: 3px 0;
            text-align: center;
            font-size: 0.7rem;
            font-weight: bold;
            border-radius: 8px 8px 0 0;
        }
        
        /* Job Map */
        .job-map-container {
            margin: 2rem 0;
            height: 400px;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            border: 1px solid #ddd;
        }
        
        #job-map {
            height: 100%;
            width: 100%;
        }

/* Location status message */
#location-status {
    color: var(--primary-blue);
    font-style: italic;
}

/* Loading spinner */
.location-loading {
    display: inline-block;
    width: 16px;
    height: 16px;
    border: 2px solid rgba(0,0,0,0.1);
    border-radius: 50%;
    border-top-color: var(--primary-blue);
    animation: spin 1s ease-in-out infinite;
    margin-right: 5px;
}

@keyframes spin {
    to { transform: rotate(360deg); }
}
        
/* Map Legend Styles */
.map-legend {
    background-color: var(--white);
    padding: 15px;
    border-radius: 8px;
    margin-bottom: 20px;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    border: 1px solid #ddd;
}

.map-legend h4 {
    margin-top: 0;
    margin-bottom: 10px;
    color: var(--primary-blue);
}

.legend-items {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
}

.legend-item {
    display: flex;
    align-items: center;
    gap: 5px;
    font-size: 0.9rem;
}

.legend-icon {
    display: inline-block;
    width: 15px;
    height: 15px;
    border-radius: 50%;
    border: 2px solid white;
}

/* Update the legend icon colors in your CSS */
.legend-icon.construction { background-color: #FFA500; } /* Construction - Orange */
.legend-icon.energy { background-color: #FF0000; }      /* Energy - Red */
.legend-icon.finance { background-color: #006400; }     /* Finance - Dark Green */
.legend-icon.healthcare { background-color: #0000FF; }  /* Healthcare - Blue */
.legend-icon.hospitality { background-color: #9400D3; } /* Hospitality - Violet */
.legend-icon.it { background-color: #808080; }          /* IT - Gray */
.legend-icon.manufacturing { background-color: #000000; } /* Manufacturing - Black */
.legend-icon.agriculture { background-color: #4CAF50; }  /* Agriculture - Green */
.legend-icon.education { background-color: #2196F3; }    /* Education - Blue */
.legend-icon.mining { background-color: #795548; }       /* Mining - Brown */
.legend-icon.retail { background-color: #FFD700; }      /* Retail - Pure Yellow (#FFFF00) */
.legend-icon.transportation { background-color: #FFFF00; } /* Transportation - Gold (#FFD700) */ 
.legend-icon.other { background-color: #9E9E9E; }        /* Other - Gray */

@media (max-width: 768px) {
    .legend-items {
        gap: 8px;
    }
    .legend-item {
        font-size: 0.8rem;
    }
}
        /* Admin Panel */
        .admin-panel {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            z-index: 9999;
            justify-content: center;
            align-items: center;
        }
        
        .admin-panel.active {
            display: flex;
        }
        
        .admin-form {
            background-color: var(--white);
            padding: 2rem;
            border-radius: 8px;
            width: 90%;
            max-width: 800px;
            max-height: 90vh;
            overflow-y: auto;
            position: relative;
        }
        
        .admin-close {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #777;
        }
        
        .admin-form h2 {
            text-align: center;
            margin-bottom: 1.5rem;
            color: var(--primary-blue);
        }
        
        .admin-form .form-group {
            margin-bottom: 1rem;
        }
        
        .admin-form label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 500;
        }
        
        .admin-form input, .admin-form select, .admin-form textarea {
            width: 100%;
            padding: 0.8rem;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
        }
        
        .admin-form textarea {
            height: 100px;
            resize: vertical;
        }
        
        .admin-form .btn {
            width: 100%;
            margin-top: 1rem;
        }

        /* Admin search bar */
        .admin-search-container {
            margin: 1rem 0;
        }

        .admin-search-bar {
            display: flex;
            gap: 10px;
            margin-bottom: 10px;
        }

        .admin-search-bar select {
            flex: 1;
            padding: 0.8rem;
            border: 1px solid #ddd;
            border-radius: 5px;
        }

        .admin-search-bar input {
            flex: 2;
            padding: 0.8rem;
            border: 1px solid #ddd;
            border-radius: 5px;
        }

        .admin-search-results {
            max-height: 300px;
            overflow-y: auto;
            border: 1px solid #ddd;
            border-radius: 5px;
            padding: 10px;
            margin-top: 10px;
            background-color: var(--light-gray);
        }

        .admin-job-result {
            padding: 10px;
            border-bottom: 1px solid #ddd;
        }

        .admin-job-result:last-child {
            border-bottom: none;
        }

        .admin-logout-btn {
            background-color: var(--accent-red);
            color: white;
            border: none;
            padding: 0.5rem 1rem;
            border-radius: 5px;
            cursor: pointer;
            margin-top: 1rem;
        }
        
        /* Job Application Modal */
        .application-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            z-index: 1001;
            justify-content: center;
            align-items: center;
        }
        
        .application-modal.active {
            display: flex;
        }
        
        .application-form {
            background-color: white;
            padding: 2rem;
            border-radius: 8px;
            width: 90%;
            max-width: 600px;
            max-height: 90vh;
            overflow-y: auto;
            position: relative;
        }
        
        .application-close {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #777;
        }
        
        .application-form h2 {
            color: var(--primary-blue);
            margin-bottom: 1.5rem;
            text-align: center;
        }
        
        .application-form .form-group {
            margin-bottom: 1rem;
        }
        
        .application-form label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 500;
        }
        
        .application-form input,
        .application-form textarea,
        .application-form select,
        .application-form .file-input-container {
            width: 100%;
            padding: 0.8rem;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
        }
        
        .application-form textarea {
            height: 100px;
            resize: vertical;
        }
        
        .form-actions {
            display: flex;
            justify-content: space-between;
            margin-top: 1.5rem;
        }

/* Terms and Conditions Modal */
.terms-modal {
    display: none;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.7);
    z-index: 1001;
    justify-content: center;
    align-items: center;
}

.terms-modal.active {
    display: flex;
}

.terms-content {
    background-color: white;
    padding: 2rem;
    border-radius: 8px;
    width: 90%;
    max-width: 800px;
    max-height: 80vh;
    overflow-y: auto;
    position: relative;
}

.terms-text {
    max-height: 60vh;
    overflow-y: auto;
    margin: 1rem 0;
    padding: 1rem;
    border: 1px solid #eee;
    background-color: var(--light-gray);
}

.terms-actions {
    display: flex;
    justify-content: flex-end;
    gap: 1rem;
    margin-top: 1rem;
}
        
                
        /* Footer */
        footer {
            background-color: var(--dark-gray);
            color: var(--white);
            padding: 3rem 0 1.5rem;
        }
        
        .footer-content {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 2rem;
            margin-bottom: 2rem;
        }
        
        .footer-column h3 {
            color: var(--accent-yellow);
            margin-bottom: 1.5rem;
            font-size: 1.2rem;
        }
        
        .footer-column ul {
            list-style: none;
        }
        
        .footer-column ul li {
            margin-bottom: 0.8rem;
        }
        
        .footer-column ul li a {
            color: var(--white);
            text-decoration: none;
            transition: color 0.3s;
        }
        
        .footer-column ul li a:hover {
            color: var(--accent-yellow);
        }
        
        .social-links {
            display: flex;
            gap: 15px;
            margin-top: 1rem;
        }
        
        .social-links a {
            color: var(--white);
            font-size: 1.5rem;
            transition: color 0.3s;
        }
        
        .social-links a:hover {
            color: var(--accent-yellow);
        }
        
        .copyright {
            text-align: center;
            padding-top: 1.5rem;
            border-top: 1px solid #555;
        }
        
        .footer-admin-link {
            color: var(--accent-yellow);
            text-decoration: none;
            font-weight: 500;
            margin-right: 15px;
        }
        
        .footer-employer-link {
            color: var(--accent-yellow);
            text-decoration: none;
            font-weight: 500;
        }
        
        .footer-links {
            margin-top: 1rem;
        }
        
        /* Chart Styles */
        .chart-container {
            position: relative;
            height: 300px;
            margin-bottom: 2rem;
        }
        
        .motivation-card {
            background-color: white;
            border-radius: 8px;
            padding: 1.5rem;
            margin-bottom: 1.5rem;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
            border-left: 4px solid var(--accent-yellow);
        }
        
        .motivation-card h4 {
            color: var(--primary-blue);
            margin-bottom: 1rem;
        }
        
        /* Animations */
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        
        .pulse {
            animation: pulse 2s infinite;
        }

        /* User Login Modal */
        .user-login-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            z-index: 1001;
            justify-content: center;
            align-items: center;
        }
        
        .user-login-modal.active {
            display: flex;
        }
        
        .user-login-form {
            background-color: white;
            padding: 2rem;
            border-radius: 8px;
            width: 90%;
            max-width: 500px;
            position: relative;
        }
        
        .user-login-close {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #777;
        }
        
        .user-login-form h2 {
            text-align: center;
            margin-bottom: 1.5rem;
            color: var(--primary-blue);
        }
        
        .user-login-form .form-group {
            margin-bottom: 1rem;
        }
        
        .user-login-form label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 500;
        }
        
        .user-login-form input {
            width: 100%;
            padding: 0.8rem;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
        }
        
        .user-login-form .btn {
            width: 100%;
            margin-top: 1rem;
        }
        
        .user-login-form .form-footer {
            text-align: center;
            margin-top: 1rem;
        }
        
        /* Forgot Password Modal */
        .forgot-password-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            z-index: 1001;
            justify-content: center;
            align-items: center;
        }
        
        .forgot-password-modal.active {
            display: flex;
        }
        
        .forgot-password-form {
            background-color: white;
            padding: 2rem;
            border-radius: 8px;
            width: 90%;
            max-width: 500px;
            position: relative;
        }
        
        .forgot-password-close {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #777;
        }
        
        .forgot-password-form h2 {
            text-align: center;
            margin-bottom: 1.5rem;
            color: var(--primary-blue);
        }
        
        .forgot-password-form .form-group {
            margin-bottom: 1rem;
        }
        
        .forgot-password-form label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 500;
        }
        
        .forgot-password-form input {
            width: 100%;
            padding: 0.8rem;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
        }
        
        .forgot-password-form .btn {
            width: 100%;
            margin-top: 1rem;
        }
        
        .forgot-password-form .form-footer {
            text-align: center;
            margin-top: 1rem;
        }

        /* User Registration Modal */
        .user-register-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            z-index: 1001;
            justify-content: center;
            align-items: center;
        }
        
        .user-register-modal.active {
            display: flex;
        }
        
        .user-register-form {
            background-color: white;
            padding: 2rem;
            border-radius: 8px;
            width: 90%;
            max-width: 500px;
            position: relative;
        }
        
        .user-register-close {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #777;
        }
        
        .user-register-form h2 {
            text-align: center;
            margin-bottom: 1.5rem;
            color: var(--primary-blue);
        }
        
        .user-register-form .form-group {
            margin-bottom: 1rem;
        }
        
        .user-register-form label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 500;
        }
        
        .user-register-form input {
            width: 100%;
            padding: 0.8rem;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
        }
        
        .user-register-form .btn {
            width: 100%;
            margin-top: 1rem;
        }
        
        .user-register-form .form-footer {
            text-align: center;
            margin-top: 1rem;
        }
/* Modern Profile Card Styles */
.profile-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1.5rem;
}

.profile-header h3 {
    color: var(--primary-blue);
    font-size: 1.3rem;
    display: flex;
    align-items: center;
    gap: 10px;
}

.profile-card {
    background-color: var(--white);
    border-radius: 10px;
    padding: 1.5rem;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
    display: flex;
    gap: 1.5rem;
    border: 1px solid rgba(0, 0, 0, 0.05);
}

.profile-avatar {
    width: 80px;
    height: 80px;
    background: linear-gradient(135deg, var(--primary-blue), var(--secondary-blue));
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    font-size: 2rem;
    flex-shrink: 0;
}

.profile-details {
    flex: 1;
}

.detail-row {
    display: flex;
    padding: 0.8rem 0;
    border-bottom: 1px solid rgba(0, 0, 0, 0.05);
}

.detail-row:last-child {
    border-bottom: none;
}

.detail-label {
    width: 150px;
    font-weight: 500;
    color: var(--dark-gray);
    display: flex;
    align-items: center;
    gap: 8px;
}

.detail-value {
    flex: 1;
    color: var(--text);
}

/* Dark mode adjustments */
.dark-mode .profile-card {
    background-color: var(--secondary);
    border-color: rgba(255, 255, 255, 0.1);
}

.dark-mode .detail-row {
    border-bottom-color: rgba(255, 255, 255, 0.1);
}

.dark-mode .detail-label {
    color: var(--dark-gray);
}

.dark-mode .detail-value {
    color: var(--text);
}

/* Responsive adjustments */
@media (max-width: 600px) {
    .profile-card {
        flex-direction: column;
        align-items: center;
        text-align: center;
    }
    
    .detail-row {
        flex-direction: column;
        gap: 5px;
    }
    
    .detail-label {
        width: 100%;
        justify-content: center;
    }
}

/* Responsive User Registration Modal */
@media (max-width: 768px) {
    .user-register-form {
        padding: 1rem;
        max-width: 95%;
        max-height: 90vh;
        overflow-y: auto;
    }
    
    .user-register-form .form-group {
        margin-bottom: 0.8rem;
    }
    
    .user-register-form input,
    .user-register-form select {
        padding: 0.6rem;
    }
    
    .user-register-form h2 {
        font-size: 1.5rem;
        margin-bottom: 1rem;
    }
    
    .file-input-container {
        margin-top: 0.5rem;
    }
    
    .file-input-button {
        padding: 0.5rem 1rem;
        font-size: 0.9rem;
    }
    
    .file-name {
        display: block;
        margin-left: 0;
        margin-top: 5px;
    }
    
    #register-subscribe {
        margin-right: 5px;
    }
    
    #register-subscribe + label {
        font-size: 0.9rem;
    }
    
    .user-register-close {
        top: 10px;
        right: 10px;
        font-size: 1.2rem;
    }
}
       /* User Dashboard Styles */
.user-dashboard {
    display: none;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.7);
    z-index: 1001;
    justify-content: center;
    align-items: center;
    padding: 20px;
    box-sizing: border-box;
}

.user-dashboard.active {
    display: flex;
}

.user-dashboard-content {
    background-color: white;
    border-radius: 12px;
    width: 100%;
    max-width: 800px;
    max-height: 90vh;
    overflow: hidden;
    position: relative;
    display: flex;
    flex-direction: column;
}

.user-dashboard-content h2 {
    color: var(--primary-blue);
    margin: 1.5rem 2rem 1rem;
    text-align: center;
    font-size: 1.8rem;
}

.user-dashboard-body {
    overflow-y: auto;
    padding: 0 2rem 2rem;
    flex-grow: 1;
}

.user-dashboard-close {
    position: absolute;
    top: 15px;
    right: 15px;
    background: none;
    border: none;
    font-size: 1.5rem;
    cursor: pointer;
    color: #777;
    z-index: 1;
}

.user-profile-section,
.user-resume-section,
.user-applied-jobs,
.user-saved-jobs,
.user-subscription-section {
    margin-bottom: 2rem;
}

.user-profile-info {
    background-color: var(--light-gray);
    padding: 1.5rem;
    border-radius: 5px;
    margin-bottom: 1rem;
}

.user-profile-info p {
    margin-bottom: 0.5rem;
}

/* Mobile Optimization for Registration Modal */
@media (max-width: 480px) {
    .user-register-form {
        width: 95%;
        padding: 1rem;
        max-height: 90vh;
        overflow-y: auto;
    }
    
    .user-register-form h2 {
        font-size: 1.5rem;
        margin-bottom: 1rem;
    }
    
    .user-register-form .form-group {
        margin-bottom: 0.8rem;
    }
    
    .user-register-form input {
        padding: 0.7rem;
        font-size: 0.9rem;
    }
    
    .file-input-container {
        margin-top: 0.5rem;
    }
    
    .file-input-button {
        padding: 6px 15px;
        font-size: 0.9rem;
    }
    
    .file-name {
        display: block;
        margin-left: 0;
        margin-top: 5px;
    }
    
    #register-subscribe {
        margin-right: 5px;
    }
    
    #register-subscribe + label {
        font-size: 0.9rem;
    }
    
    .user-register-form .btn {
        padding: 0.7rem;
        font-size: 1rem;
    }
    
    .form-footer p {
        font-size: 0.9rem;
    }
}

/* Mobile styles */
@media (max-width: 768px) {
    .user-dashboard-content {
        max-width: 95%;
        max-height: 95vh;
    }
    
    .user-dashboard-body {
        padding: 0 1rem 1rem;
    }
    
    .user-dashboard-content h2 {
        margin: 1rem 1rem 0.5rem;
        font-size: 1.5rem;
    }
    
    .user-profile-section,
    .user-resume-section,
    .user-applied-jobs,
    .user-saved-jobs,
    .user-subscription-section {
        margin-bottom: 1.5rem;
    }

   .header-content {
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        padding: 0 10px;
    }
    
    .logo {
        flex-direction: row;
        align-items: center;
    }
    
    .logo-text {
        margin-left: 5px;
    }

    /* Calculator button styles for mobile */
.calculator-form .btn {
    width: 100%;
    margin-bottom: 10px;
}

.calculator-form .form-row {
    flex-direction: column;
    gap: 0;
}

.calculator-form .form-row .form-group {
    margin-bottom: 1rem;
}

.calculator-tabs {
    overflow-x: auto;
    flex-wrap: nowrap;
    padding-bottom: 10px;
    -webkit-overflow-scrolling: touch;
}

.calculator-tab {
    white-space: nowrap;
    margin-right: 5px;
    margin-bottom: 0;
    font-size: 0.9rem;
    padding: 0.6rem 1rem;
}
    .hero-content .btn {
        display: inline-block;
        width: auto;
        margin: 5px;
        padding: 0.6rem 1rem;
        font-size: 0.9rem;
    }
    
    .hero-content .btn.pulse {
        margin-left: 0;
        margin-right: 5px;
    }
    
    .hero-content .btn.btn-blue.pulse {
        margin-left: 5px;
    }

    /* Optional: Adjust hero content padding */
    .hero-content {
        padding: 15px !important;
    }

    /* Better mobile menu button */
    .mobile-menu-btn {
    font-size: 1.8rem;
    padding: 5px;
    background: rgba(255,255,255,0.1);
    border-radius: 5px;
    order: 3; /* Menu button on the far right */
    margin-left: 10px;
    flex-shrink: 0;
    position: absolute;
    right: 15px;
    top: 15px;
}

    /* Improved mobile menu */
    nav ul {
        position: absolute;
        top: 100%;
        left: 0;
        right: 0;
        background: var(--secondary-blue);
        margin-top: 0;
        padding: 10px 0;
        max-height: calc(100vh - 60px);
        overflow-y: auto;
    }
    
    nav ul li {
        width: 100%;
        text-align: center;
    }
    
    nav ul li a {
        padding: 10px 15px;
        justify-content: center;
    }
    
    /* Adjust hero section for mobile */
    .hero {
        height: 300px;
        margin-top: 0;
    }
    
    .hero-content {
        padding: 20px;
    }
    
    .hero h2 {
        font-size: 1.8rem;
    }
    
    .hero p {
        font-size: 1rem;
    }
}        
        /* Admin Controls */
        .admin-controls {
            display: none;
            background-color: var(--white);
            padding: 1rem;
            margin-bottom: 1rem;
            border-radius: 5px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }
        
        .admin-controls.active {
            display: block;
        }
        
        /* Blue Collar Job Badges */
        .certification-badge {
            display: inline-block;
            background-color: var(--primary-blue);
            color: white;
            padding: 3px 8px;
            border-radius: 3px;
            font-size: 0.7rem;
            margin-right: 5px;
            margin-bottom: 5px;
        }
        
        .certification-badge.welding {
            background-color: #e67e22;
        }
        
        .certification-badge.hvac {
            background-color: #3498db;
        }
        
        .certification-badge.osh {
            background-color: #e74c3c;
        }
        
        .certification-badge.offshore {
            background-color: #9b59b6;
        }
        
        /* Manual Search Bars */
        .manual-search-container {
            margin: 1rem 0;
            padding: 1rem;
            background-color: var(--white);
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }
        
        .manual-search-group {
            margin-bottom: 1rem;
        }
        
        .manual-search-group label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 500;
        }
        
        .manual-search-group input {
            width: 100%;
            padding: 0.8rem;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
        }
        
        .manual-search-group input:focus {
            border-color: var(--primary-blue);
            box-shadow: 0 0 0 3px rgba(0, 102, 204, 0.2);
            outline: none;
        }
        
        /* File input styling */
        .file-input-container {
            position: relative;
            overflow: hidden;
            display: inline-block;
            width: 100%;
        }
        
        .file-input-button {
            background-color: var(--primary-blue);
            color: white;
            padding: 8px 20px;
            border-radius: 5px;
            font-size: 1rem;
            font-weight: 500;
            cursor: pointer;
            display: inline-block;
        }
        
        .file-input {
            position: absolute;
            left: 0;
            top: 0;
            opacity: 0;
            width: 100%;
            height: 100%;
            cursor: pointer;
        }
        
        .file-name {
            margin-left: 10px;
            font-size: 0.9rem;
            color: #666;
        }
        
        /* User settings button */
        .user-settings-btn {
            background-color: var(--primary-blue);
            color: white;
            border: none;
            padding: 0.5rem 1rem;
            border-radius: 5px;
            cursor: pointer;
            margin-top: 1rem;
            display: inline-block;
        }
        
        /* Company Modal */
        .company-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            z-index: 1001;
            justify-content: center;
            align-items: center;
        }
        
        .company-modal.active {
            display: flex;
        }
        
        .company-content {
            background-color: white;
            padding: 2rem;
            border-radius: 8px;
            width: 90%;
            max-width: 800px;
            max-height: 90vh;
            overflow-y: auto;
            position: relative;
        }
        
        .company-close {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #777;
        }
        
        .company-header {
            display: flex;
            align-items: center;
            margin-bottom: 1.5rem; 
        }
        
        .company-logo {
    width: 80px;
    height: 80px;
    background-color: var(--light-gray);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-right: 1.5rem;
    overflow: hidden;
}

.company-logo img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

#company-verification-control {
    text-align: center;
    padding: 0.5rem;
    background-color: var(--light-gray);
    border-radius: 5px;
}

#toggle-company-verification {
    width: 100%;
    max-width: 200px;
}
        
        .company-info h2 {
            color: var(--primary-blue);
            margin-bottom: 0.5rem;
        }
        
        .company-info p {
            color: #666;
            margin-bottom: 0.5rem;
        }
        
        .company-bio {
            margin-bottom: 1.5rem;
            line-height: 1.6;
        }
        
        .company-jobs h3 {
            color: var(--primary-blue);
            margin-bottom: 1rem;
        }
        
        .company-jobs-list {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 1rem;
        }
        
        .company-job-card {
            background-color: var(--light-gray);
            padding: 1rem;
            border-radius: 5px;
            border: 1px solid #ddd;
        }
        
        .company-job-card h4 {
            color: var(--primary-blue);
            margin-bottom: 0.5rem;
        }
        
        /* Company Management Modal */
        .company-management-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            z-index: 1001;
            justify-content: center;
            align-items: center;
        }
        
        .company-management-modal.active {
            display: flex;
        }
        
        .company-management-form {
    background-color: var(--white);
    border-radius: 12px;
    padding: 2rem;
    width: 90%;
    max-width: 800px;
    max-height: 90vh;
    overflow-y: auto;
    position: relative;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
}

.company-management-form h2 {
    color: var(--primary-blue);
    margin-bottom: 1.5rem;
    text-align: center;
    font-size: 1.8rem;
    font-weight: 600;
}

.company-management-form .form-group {
    margin-bottom: 1.5rem;
    position: relative;
}

.company-management-form label {
    display: block;
    margin-bottom: 0.5rem;
    font-weight: 600;
    color: var(--dark-gray);
    font-size: 0.95rem;
}

.company-management-form input,
.company-management-form select,
.company-management-form textarea {
    width: 100%;
    padding: 0.8rem 1rem;
    border: 2px solid #e0e0e0;
    border-radius: 8px;
    font-size: 1rem;
    transition: all 0.3s ease;
    background-color: var(--light-gray);
}

.company-management-form input:focus,
.company-management-form select:focus,
.company-management-form textarea:focus {
    border-color: var(--primary-blue);
    box-shadow: 0 0 0 3px rgba(0, 102, 204, 0.1);
    outline: none;
    background-color: var(--white);
}

.company-management-form textarea {
    height: 120px;
    resize: vertical;
}

.company-form-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1.5rem;
    margin-bottom: 1.5rem;
}

.company-logo-upload {
    display: flex;
    align-items: center;
    gap: 1rem;
    margin-bottom: 1.5rem;
}

.company-logo-preview {
    width: 80px;
    height: 80px;
    border-radius: 8px;
    background-color: var(--light-gray);
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    border: 2px dashed #ccc;
}

.company-logo-preview img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.company-verified-toggle {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    margin-bottom: 1.5rem;
}

.company-verified-toggle label {
    margin-bottom: 0;
    font-weight: 500;
}

.company-form-actions {
    display: flex;
    justify-content: space-between;
    gap: 1rem;
    margin-top: 2rem;
}

.company-form-actions .btn {
    flex: 1;
    padding: 0.8rem;
    font-weight: 600;
    border-radius: 8px;
}
        
        .company-management-close {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #777;
        }
        
        /* Advertisement Slideshow */
        .advertisement-section {
            margin: 3rem 0;
            padding: 1rem;
        }
        
        .ad-container {
            position: relative;
            width: 100%;
            height: 300px;
            overflow: hidden;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        
        .ad-slide {
            position: absolute;
            width: 100%;
            height: 100%;
            opacity: 0;
            transition: opacity 1s ease-in-out;
        }
        
        .ad-slide.active {
            opacity: 1;
        }
        
        .ad-slide img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            cursor: pointer;
        }
        
        .ad-nav {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            background-color: rgba(0, 0, 0, 0.5);
            color: white;
            border: none;
            padding: 1rem;
            cursor: pointer;
            z-index: 10;
            font-size: 1.5rem;
        }
        
        .ad-nav.prev {
            left: 0;
            border-radius: 0 5px 5px 0;
        }
        
        .ad-nav.next {
            right: 0;
            border-radius: 5px 0 0 5px;
        }
        
        .ad-nav:hover {
            background-color: rgba(0, 0, 0, 0.7);
        }
        
        /* Advertisement Management Modal */
        .ad-management-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            z-index: 1001;
            justify-content: center;
            align-items: center;
        }
        
        .ad-management-modal.active {
            display: flex;
        }
        
        .ad-management-form {
            background-color: white;
            padding: 2rem;
            border-radius: 8px;
            width: 90%;
            max-width: 800px;
            max-height: 90vh;
            overflow-y: auto;
            position: relative;
        }
        
        .ad-management-close {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #777;
        }
        
        /* Pagination */
        .pagination {
            display: flex;
            justify-content: center;
            margin-top: 2rem;
            gap: 5px;
        }
        
        .page-btn {
            padding: 8px 12px;
            border: 1px solid #ddd;
            background-color: white;
            cursor: pointer;
            border-radius: 5px;
        }
        
        .page-btn.active {
            background-color: var(--primary-blue);
            color: white;
            border-color: var(--primary-blue);
        }
        
        .page-btn:hover:not(.active) {
            background-color: #f0f0f0;
        }

/* Admin Dashboard */
.admin-dashboard-modal {
    display: none;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.7);
    z-index: 1001;
    justify-content: center;
    align-items: center;
}

.admin-dashboard-modal.active {
    display: flex;
}

.admin-dashboard-content {
    background-color: var(--white);
    padding: 2rem;
    border-radius: 8px;
    width: 90%;
    max-width: 900px;
    max-height: 90vh;
    overflow-y: auto;
    position: relative;
}

.admin-dashboard-close {
    position: absolute;
    top: 15px;
    right: 15px;
    background: none;
    border: none;
    font-size: 1.5rem;
    cursor: pointer;
    color: #777;
}

.dashboard-stats {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1rem;
    margin-bottom: 2rem;
}

.stat-card {
    background-color: var(--light-gray);
    padding: 1.5rem;
    border-radius: 8px;
    text-align: center;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.stat-card h3 {
    color: var(--primary-blue);
    margin-bottom: 0.5rem;
    font-size: 1.1rem;
}

.stat-card p {
    font-size: 2rem;
    font-weight: bold;
    color: var(--dark-gray);
}

.dashboard-charts {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1.5rem;
}

.chart-container {
    background-color: var(--light-gray);
    padding: 1.5rem;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.chart-container h3 {
    color: var(--primary-blue);
    margin-bottom: 1rem;
    text-align: center;
}

@media (max-width: 768px) {
    .dashboard-charts {
        grid-template-columns: 1fr;
    }
}
        
        /* Save Job Button */
        .save-job-btn {
            background: none;
            border: none;
            cursor: pointer;
            font-size: 1.2rem;
            color: #ccc;
            transition: color 0.3s;
            padding: 5px;
        }
        
        .save-job-btn.saved {
            color: var(--accent-yellow);
        }
        
        .save-job-btn:hover {
            color: var(--accent-yellow);
        }

/* Job Comparison Styles */
        .comparison-section {
            background-color: var(--white);
            padding: 3rem 0;
            margin-top: 2rem;
            border-top: 1px solid #eee;
        }
        
        .comparison-controls {
            display: flex;
            gap: 10px;
            margin-bottom: 1.5rem;
            flex-wrap: wrap;
        }
        
        .comparison-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 1.5rem;
            margin-top: 1rem;
        }
        
        .comparison-job {
            background-color: var(--light-gray);
            border-radius: 8px;
            padding: 1.5rem;
            border: 1px solid #ddd;
            position: relative;
        }
        
        .comparison-job h3 {
            color: var(--primary-blue);
            margin-bottom: 0.5rem;
        }
        
        .comparison-job .company {
            font-weight: 600;
            color: var(--secondary-blue);
            margin-bottom: 0.5rem;
        }
        
        .comparison-job .remove-comparison {
            position: absolute;
            top: 10px;
            right: 10px;
            background: none;
            border: none;
            color: var(--accent-red);
            cursor: pointer;
            font-size: 1.2rem;
        }
        
        .comparison-job .job-detail {
            margin-bottom: 0.5rem;
            padding-bottom: 0.5rem;
            border-bottom: 1px solid #eee;
        }
        
        .comparison-job .job-detail strong {
            display: block;
            color: var(--dark-gray);
            margin-bottom: 0.2rem;
        }
        
        .empty-message {
            text-align: center;
            grid-column: 1 / -1;
            color: #666;
            padding: 2rem;
        }
        
       .job-checkbox {
    position: absolute;
    top: 5px;
    left: 10px;
    width: 16px;
    height: 16px;
    z-index: 2; /* Ensure it's above the pinned badge */
    margin: 0;
    cursor: pointer;
}

/* Adjust position when pinned badge is present */
.job-card .pinned-badge ~ .job-checkbox {
    top: 30px; /* Below the pinned badge */
}
        
        .job-card {
            position: relative;
        }

/* Job Checkbox Styling */
.job-checkbox {
    position: absolute;
    top: 5px;
    left: 10px;
    width: 16px;
    height: 16px;
    z-index: 2;
    margin: 0;
    cursor: pointer;
    accent-color: var(--light-gray); /* Default to job card background */
}

/* When pinned badge is present */
.job-card .pinned-badge ~ .job-checkbox {
    top: 30px;
    accent-color: var(--accent-yellow); /* Match pinned badge color */
}

/* Dark mode adjustments */
.dark-mode .job-checkbox {
    accent-color: var(--secondary); /* Dark mode job card background */
}

.dark-mode .job-card .pinned-badge ~ .job-checkbox {
    accent-color: var(--accent-yellow); /* Keep yellow in dark mode */
}

/* High contrast mode adjustments */
.high-contrast .job-checkbox {
    accent-color: var(--light-gray);
}

.high-contrast .job-card .pinned-badge ~ .job-checkbox {
    accent-color: var(--accent-yellow);
}

/* Low contrast mode adjustments */
.low-contrast .job-checkbox {
    accent-color: var(--light-gray);
}

.low-contrast .job-card .pinned-badge ~ .job-checkbox {
    accent-color: var(--accent-yellow);
}


/* Fix for list view buttons */
.jobs-container.list-view .job-card .job-actions {
    flex-direction: column;
    align-items: flex-end;
    margin-top: 15px;
    gap: 8px;
}

.jobs-container.list-view .job-card .job-actions .btn {
    width: auto;
    min-width: 120px;
}

/* Fix for compact view pinned badge overlap */
.jobs-container.compact-view .job-card {
    position: relative;
    padding-top: 28px; /* Add space for pinned badge */
}

.jobs-container.compact-view .job-card .pinned-badge {
    top: 0;
    left: 0;
    right: 0;
    border-radius: 8px 8px 0 0;
}

/* Mobile optimization for list view */
@media (max-width: 768px) {
    .jobs-container.list-view .job-card {
        flex-direction: column;
        padding: 1rem;
    }
    
    .jobs-container.list-view .job-card > * {
        margin-bottom: 0.5rem;
    }
    
    .jobs-container.list-view .job-card h3 {
        margin-right: 0;
        min-width: auto;
        font-size: 1.1rem;
    }
    
    .jobs-container.list-view .job-card .job-meta {
        flex-direction: row;
        justify-content: space-between;
        font-size: 0.8rem;
    }
    
    .jobs-container.list-view .job-card .job-actions {
        flex-direction: row;
        align-items: center;
        justify-content: flex-start;
        margin-top: 0.5rem;
        gap: 5px;
    }
    
    .jobs-container.list-view .job-card .job-actions .btn {
        min-width: auto;
        padding: 0.5rem;
        font-size: 0.9rem;
    }
    
    .jobs-container.list-view .job-card .description,
    .jobs-container.list-view .job-card .requirements {
        display: none;
    }
    
    .jobs-container.list-view .job-card .certifications {
        display: flex;
        flex-wrap: wrap;
        gap: 5px;
        margin-bottom: 0.5rem;
    }
    
    .jobs-container.list-view .job-card .certification-badge {
        font-size: 0.6rem;
        padding: 2px 5px;
    }
    
    .jobs-container.list-view .job-card .deadline {
        font-size: 0.8rem;
    }
    
    .jobs-container.list-view .job-card .save-job-btn {
        font-size: 1rem;
    }
@media (max-width: 768px) {
    .jobs-container.list-view .job-card {
        position: relative;
        padding-top: 28px; /* Add space for pinned badge */
    }
    
    .jobs-container.list-view .job-card .pinned-badge {
        top: 0;
        left: 0;
        right: 0;
        border-radius: 8px 8px 0 0;
    }
}

        
        /* Responsive Styles */
        @media (max-width: 768px) {
            .header-content {
                flex-direction: column;
                text-align: center;
            }
            
            nav ul {
                margin-top: 1rem;
                flex-direction: column;
                align-items: center;
                display: none;
            }
            
            nav ul.show {
                display: flex;
            }
            
            nav ul li {
                margin: 0.5rem 0;
            }
            
            .hero {
                height: 400px;
                margin-top: -60px;
            }
            
            .hero h2 {
                font-size: 2rem;
            }
            
            .features {
                grid-template-columns: 1fr;
            }

            .form-row {
                flex-direction: column;
                gap: 0;
            }

            .jobs-container {
                grid-template-columns: 1fr;
            }
            
            .calculator-tabs {
                overflow-x: auto;
                flex-wrap: nowrap;
                padding-bottom: 10px;
            }
            
            .calculator-tab {
                white-space: nowrap;
            }
            
            .mobile-menu-btn {
                display: block;
            }

            .mobile-menu-btn {
                display: block;
            }
            
            /* Mobile dropdown styles */
            .dropdown-content {
                position: static;
                display: none;
                width: 100%;
                box-shadow: none;
            }
            
            .dropdown:hover .dropdown-content {
                display: none;
            }
            
            .dropdown.active .dropdown-content {
                display: block;
            }
            
            .company-jobs-list {
                grid-template-columns: 1fr;
            }
            
            .company-header {
                flex-direction: column;
                text-align: center;
            }
            
            .company-logo {
                margin-right: 0;
                margin-bottom: 1rem;
            }
        }       
    </style>
</head>
<body>
    <!-- Header with Navigation -->
    <header>
        <div class="container header-content">
            <a href="#" class="logo home-link">
                <div class="logo-img">
                    <i class="fas fa-hard-hat"></i>
                </div>
                <div class="logo-text">
                    <div class="logo-main">WorkRight<span>TT</span></div>
                    <div class="logo-sub">Find Your Perfect Job</div>
                </div>
            </a>
            
            <button class="mobile-menu-btn">
                <i class="fas fa-bars"></i>
            </button>
            
            <nav>
                <ul>
                    <li><a href="#jobs-section"><i class="fas fa-briefcase"></i> Jobs</a></li>
                    <li class="dropdown">
                        <a href="#"><i class="fas fa-tools"></i> Tools <i class="fas fa-chevron-down"></i></a>
                        <div class="dropdown-content">
                            <a href="#comparison-tool">Comparison Tool</a>
                        </div>
                    </li>
                    <li><a href="#about-us"><i class="fas fa-info-circle"></i> About Us</a></li>
                    <li><a href="#" id="login-btn"><i class="fas fa-sign-in-alt"></i> Login</a></li>
                </ul>
            </nav>
        </div>
    </header>

    <!-- Hero Section -->
    <section class="hero">
        <div class="container hero-content">
            <h2>Find Your Perfect Job in Trinidad & Tobago</h2>
            <p>Discover opportunities across various industries with WorkRightTT</p>
            <a href="#jobs-section" class="btn pulse">Browse Jobs</a>
        </div>
    </section>

    <!-- Advertisement Section -->
    <section class="advertisement-section">
        <div class="container">
            <div class="ad-container">
                <div class="ad-slide active">
                    <img src="https://via.placeholder.com/1200x300/0066cc/ffffff?text=WorkRightTT+Advertisement+1" alt="Advertisement 1">
                </div>
                <div class="ad-slide">
                    <img src="https://via.placeholder.com/1200x300/004d99/ffffff?text=WorkRightTT+Advertisement+2" alt="Advertisement 2">
                </div>
                <button class="ad-nav prev"><i class="fas fa-chevron-left"></i></button>
                <button class="ad-nav next"><i class="fas fa-chevron-right"></i></button>
            </div>
        </div>
    </section>

    <!-- Job Search Section -->
    <section id="jobs-section" class="jobs-section">
        <div class="container">
            <div class="section-title">
                <h2>Job Opportunities</h2>
                <p>Find your next career move with our comprehensive job search</p>
            </div>

            <!-- Manual Search Bars -->
            <div class="manual-search-container">
                <div class="form-row">
                    <div class="form-group">
                        <label for="job-title-search">Job Title</label>
                        <input type="text" id="job-title-search" placeholder="e.g. Welder, Electrician, Nurse">
                    </div>
                    <div class="form-group">
                        <label for="company-search">Company</label>
                        <input type="text" id="company-search" placeholder="e.g. Company Name">
                    </div>
                    <div class="form-group">
                        <label for="certification-search">Certification</label>
                        <input type="text" id="certification-search" placeholder="e.g. OSHA, First Aid">
                    </div>
                </div>
                <div class="form-row">
                    <button id="search-jobs-btn" class="btn btn-blue">Search Jobs</button>
                    <button id="reset-search-btn" class="btn">Reset</button>
                </div>
            </div>

            <!-- Advanced Filters Toggle -->
            <div class="filter-toggle-container">
                <button id="toggle-advanced-filters-btn" class="btn">
                    <i class="fas fa-filter"></i> Show More Filters
                </button>
            </div>

            <!-- Advanced Filters (Initially Hidden) -->
            <div id="advanced-filters" class="advanced-filters-container" style="display: none;">
                <div class="form-row">
                    <div class="form-group">
                        <label for="industry-filter">Industry</label>
                        <select id="industry-filter">
                            <option value="">All Industries</option>
                            <option value="agriculture">Agriculture</option>
                            <option value="construction">Construction</option>
                            <option value="education">Education</option>
                            <option value="energy">Energy</option>
                            <option value="finance">Finance</option>
                            <option value="healthcare">Healthcare</option>
                            <option value="hospitality">Hospitality</option>
                            <option value="it">Information Technology</option>
                            <option value="manufacturing">Manufacturing</option>
                            <option value="mining">Mining</option>
                            <option value="other">Other</option>
                            <option value="retail">Retail</option>
                            <option value="transport">Transport</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label for="region-filter">Region</label>
                        <select id="region-filter">
                            <option value="">All Regions</option>
                            <option value="north">North (Port of Spain, Diego Martin, etc.)</option>
                            <option value="central">Central (Chaguanas, Couva, Freeport, etc.)</option>
                            <option value="south">South (San Fernando, Point Fortin, etc.)</option>
                            <option value="tobago">Tobago</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label for="location-type-filter">Work Location Type</label>
                        <select id="location-type-filter">
                            <option value="">Any Location Type</option>
                            <option value="onsite">On Site</option>
                            <option value="hybrid">Hybrid</option>
                            <option value="remote">Remote</option>
                            <option value="wfh">Work from Home</option>
                        </select>
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label for="salary-range-filter">Salary Range</label>
                        <select id="salary-range-filter">
                            <option value="">Any Salary</option>
                            <option value="0-3000">$0 to $3000 TTD</option>
                            <option value="3000-6000">$3000 to $6000 TTD</option>
                            <option value="6000-10000">$6000 to $10000 TTD</option>
                            <option value="10000+">$10000 TTD +</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label for="salary-period-filter">Salary Period</label>
                        <select id="salary-period-filter">
                            <option value="">Any Period</option>
                            <option value="month">Per Month</option>
                            <option value="week">Per Week</option>
                            <option value="day">Per Day</option>
                            <option value="hour">Per Hour</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label for="employment-type-filter">Employment Type</label>
                        <select id="employment-type-filter">
                            <option value="">Any Type</option>
                            <option value="full-time">Full-time</option>
                            <option value="part-time">Part-time</option>
                            <option value="contract">Contract</option>
                            <option value="temporary">Temporary</option>
                            <option value="internship">Internship</option>
                        </select>
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label for="posted-within-filter">Posted Within</label>
                        <select id="posted-within-filter">
                            <option value="">Anytime</option>
                            <option value="1">Last 24 hours</option>
                            <option value="7">Last week</option>
                            <option value="30">Last month</option>
                        </select>
                    </div>
                </div>
            </div>

            <!-- Location & Map Filters Toggle -->
            <div class="filter-toggle-container" id="location-toggle-container">
                <button id="toggle-location-filters-btn" class="btn">
                    <i class="fas fa-map-marker-alt"></i> Show Location & Map Filters
                </button>
            </div>

            <!-- Location & Map Filters (Initially Hidden) -->
            <div id="location-filters" class="advanced-filters-container" style="display: none;">
                <div class="form-row">
                    <div class="form-group">
                        <label for="isochrone-filter">Maximum Drive Time (Minutes)</label>
                        <select id="isochrone-filter">
                            <option value="0">No limit</option>
                            <option value="15">15 min</option>
                            <option value="30">30 min</option>
                            <option value="60">60 min</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>&nbsp;</label>
                        <button id="use-my-location-btn" class="btn">
                            <i class="fas fa-location-arrow"></i> Use My Location
                        </button>
                        <span id="location-status"></span>
                    </div>
                </div>
            </div>

            <!-- Map Legend -->
            <div class="map-legend">
                <h4>Industry Legend</h4>
                <div class="legend-items">
                    <div class="legend-item">
                        <span class="legend-icon construction"></span>
                        <span>Construction</span>
                    </div>
                    <div class="legend-item">
                        <span class="legend-icon energy"></span>
                        <span>Energy</span>
                    </div>
                    <div class="legend-item">
                        <span class="legend-icon finance"></span>
                        <span>Finance</span>
                    </div>
                    <div class="legend-item">
                        <span class="legend-icon healthcare"></span>
                        <span>Healthcare</span>
                    </div>
                    <div class="legend-item">
                        <span class="legend-icon hospitality"></span>
                        <span>Hospitality</span>
                    </div>
                    <div class="legend-item">
                        <span class="legend-icon it"></span>
                        <span>IT</span>
                    </div>
                    <div class="legend-item">
                        <span class="legend-icon manufacturing"></span>
                        <span>Manufacturing</span>
                    </div>
                    <div class="legend-item">
                        <span class="legend-icon agriculture"></span>
                        <span>Agriculture</span>
                    </div>
                    <div class="legend-item">
                        <span class="legend-icon education"></span>
                        <span>Education</span>
                    </div>
                    <div class="legend-item">
                        <span class="legend-icon mining"></span>
                        <span>Mining</span>
                    </div>
                    <div class="legend-item">
                        <span class="legend-icon retail"></span>
                        <span>Retail</span>
                    </div>
                    <div class="legend-item">
                        <span class="legend-icon transportation"></span>
                        <span>Transportation</span>
                    </div>
                    <div class="legend-item">
                        <span class="legend-icon other"></span>
                        <span>Other</span>
                    </div>
                </div>
            </div>

            <!-- Job Map -->
            <div class="job-map-container">
                <div id="job-map"></div>
            </div>

            <!-- View Options -->
            <div class="grid-style-container">
                <span>View:</span>
                <button class="grid-style-btn active" data-view="grid">
                    <i class="fas fa-th"></i> Grid
                </button>
                <button class="grid-style-btn" data-view="list">
                    <i class="fas fa-list"></i> List
                </button>
                <button class="grid-style-btn" data-view="compact">
                    <i class="fas fa-grip-horizontal"></i> Compact
                </button>
            </div>

            <!-- Admin Controls (Visible only to admins) -->
            <div id="admin-controls" class="admin-controls">
                <h3>Admin Controls</h3>
                <div class="form-row">
                    <button id="add-job-btn" class="btn btn-blue">Add New Job</button>
                    <button id="manage-companies-btn" class="btn btn-blue">Manage Companies</button>
                    <button id="manage-ads-btn" class="btn btn-blue">Manage Ads</button>
                    <button id="edit-jobs-btn" class="btn btn-blue">Edit Jobs</button>
                    <button id="dashboard-btn" class="btn btn-blue">Dashboard</button>
                </div>
            </div>

            <!-- Jobs Container -->
            <div id="jobs-container" class="jobs-container grid-view">
                <!-- Job cards will be dynamically inserted here -->
                <div class="loading">Loading jobs...</div>
            </div>

            <!-- Pagination -->
            <div class="pagination">
                <button class="page-btn prev"><i class="fas fa-chevron-left"></i> Previous</button>
                <button class="page-btn active">1</button>
                <button class="page-btn">2</button>
                <button class="page-btn">3</button>
                <button class="page-btn next">Next <i class="fas fa-chevron-right"></i></button>
            </div>

            <!-- Go to Page -->
            <div class="manual-search-container">
                <div class="form-row">
                    <div class="form-group">
                        <label for="go-to-page">Go to Page</label>
                        <input type="number" id="go-to-page" min="1" placeholder="Page number">
                    </div>
                    <button id="go-to-page-btn" class="btn">Go</button>
                </div>
            </div>
        </div>
    </section>

    <!-- Comparison Tool Section -->
    <section id="comparison-tool" class="comparison-section">
        <div class="container">
            <div class="section-title">
                <h2>Job Comparison Tool</h2>
                <p>Compare up to 5 jobs side by side</p>
            </div>

            <div class="comparison-controls">
                <button id="clear-comparison-btn" class="btn btn-red">Clear All</button>
                <span id="comparison-count">0/5 jobs selected</span>
            </div>

            <div id="comparison-container" class="comparison-container">
                <div class="empty-message">
                    <p>No jobs selected for comparison. Select jobs using the checkboxes on job cards.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- About Us Section -->
    <section id="about-us" class="features">
        <div class="container">
            <div class="section-title">
                <h2>About WorkRightTT</h2>
                <p>Connecting job seekers with employers across Trinidad and Tobago</p>
            </div>
            
            <div class="feature-card">
                <i class="fas fa-bullseye"></i>
                <h3>Our Mission</h3>
                <p>To provide a comprehensive platform that connects qualified candidates with the right job opportunities in Trinidad and Tobago.</p>
            </div>
            
            <div class="feature-card">
                <i class="fas fa-eye"></i>
                <h3>Our Vision</h3>
                <p>To be the leading job portal in Trinidad and Tobago, recognized for excellence in connecting talent with opportunity.</p>
            </div>
            
            <div class="feature-card">
                <i class="fas fa-handshake"></i>
                <h3>Our Values</h3>
                <p>Integrity, innovation, and commitment to both job seekers and employers in the Trinidad and Tobago job market.</p>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer>
        <div class="container">
            <div class="footer-content">
                <div class="footer-column">
                    <h3>WorkRightTT</h3>
                    <p>Connecting job seekers with employers across Trinidad and Tobago.</p>
                    <div class="social-links">
                        <a href="#"><i class="fab fa-facebook"></i></a>
                        <a href="#"><i class="fab fa-twitter"></i></a>
                        <a href="#"><i class="fab fa-instagram"></i></a>
                        <a href="#"><i class="fab fa-linkedin"></i></a>
                    </div>
                </div>
                
                <div class="footer-column">
                    <h3>Quick Links</h3>
                    <ul>
                        <li><a href="#jobs-section">Browse Jobs</a></li>
                        <li><a href="#comparison-tool">Comparison Tool</a></li>
                        <li><a href="#about-us">About Us</a></li>
                        <li><a href="#">Privacy Policy</a></li>
                        <li><a href="#">Terms of Service</a></li>
                    </ul>
                </div>
                
                <div class="footer-column">
                    <h3>Resources</h3>
                    <ul>
                        <li><a href="#">Resume Tips</a></li>
                        <li><a href="#">Interview Preparation</a></li>
                        <li><a href="#">Career Advice</a></li>
                        <li><a href="#">Industry Insights</a></li>
                    </ul>
                </div>
                
                <div class="footer-column">
                    <h3>Contact Us</h3>
                    <ul>
                        <li><i class="fas fa-envelope"></i> info@workrighttt.com</li>
                        <li><i class="fas fa-phone"></i> +1 (868) 123-4567</li>
                        <li><i class="fas fa-map-marker-alt"></i> Port of Spain, Trinidad</li>
                    </ul>
                </div>
            </div>
            
            <div class="footer-links">
                <a href="#" class="footer-admin-link">Employer Login</a>
                <a href="#" class="footer-employer-link">Post a Job</a>
            </div>
            
            <div class="copyright">
                <p>&copy; 2023 WorkRightTT. All rights reserved.</p>
            </div>
        </div>
    </footer>

    <!-- Floating Controls -->
    <div class="floating-controls-container">
        <div class="floating-controls-buttons">
            <button class="accessibility-toggle btn">
                <i class="fas fa-universal-access"></i>
            </button>
            <button class="language-toggle btn">
                <i class="fas fa-globe"></i>
            </button>
        </div>
        <button class="floating-controls-main-toggle">
            <i class="fas fa-cog"></i>
        </button>
    </div>

    <!-- Dark Mode Toggle -->
    <button class="dark-mode-toggle">
        <i class="fas fa-moon"></i>
    </button>

    <!-- Login Modal -->
    <div class="user-login-modal">
        <div class="user-login-form">
            <button class="user-login-close">&times;</button>
            <h2>Login to WorkRightTT</h2>
            <div class="form-group">
                <label for="login-email">Email</label>
                <input type="email" id="login-email" placeholder="Your email">
            </div>
            <div class="form-group">
                <label for="login-password">Password</label>
                <input type="password" id="login-password" placeholder="Your password">
            </div>
            <button id="login-submit-btn" class="btn btn-blue">Login</button>
            <div class="form-footer">
                <p>Don't have an account? <a href="#" id="register-link">Register here</a></p>
                <p><a href="#" id="forgot-password-link">Forgot password?</a></p>
            </div>
        </div>
    </div>

    <!-- Registration Modal -->
    <div class="user-register-modal">
        <div class="user-register-form">
            <button class="user-register-close">&times;</button>
            <h2>Create an Account</h2>
            <div class="form-group">
                <label for="register-name">Full Name</label>
                <input type="text" id="register-name" placeholder="Your full name">
            </div>
            <div class="form-group">
                <label for="register-email">Email</label>
                <input type="email" id="register-email" placeholder="Your email">
            </div>
            <div class="form-group">
                <label for="register-password">Password</label>
                <input type="password" id="register-password" placeholder="Create a password">
            </div>
            <div class="form-group">
                <label for="register-confirm-password">Confirm Password</label>
                <input type="password" id="register-confirm-password" placeholder="Confirm your password">
            </div>
            <div class="form-group">
                <label>Resume (Required)</label>
                <div class="file-input-container">
                    <div class="file-input-button">Choose File</div>
                    <input type="file" class="file-input" id="register-resume" accept=".pdf,.doc,.docx">
                    <span class="file-name" id="resume-file-name">No file chosen</span>
                </div>
            </div>
            <div class="form-group">
                <input type="checkbox" id="register-subscribe">
                <label for="register-subscribe">Subscribe to job alerts</label>
            </div>
            <div class="form-group">
                <input type="checkbox" id="register-terms">
                <label for="register-terms">I agree to the <a href="#" id="terms-link">Terms and Conditions</a></label>
            </div>
            <button id="register-submit-btn" class="btn btn-blue">Create Account</button>
            <div class="form-footer">
                <p>Already have an account? <a href="#" id="login-link">Login here</a></p>
            </div>
        </div>
    </div>

    <!-- Forgot Password Modal -->
    <div class="forgot-password-modal">
        <div class="forgot-password-form">
            <button class="forgot-password-close">&times;</button>
            <h2>Reset Password</h2>
            <div class="form-group">
                <label for="forgot-email">Email</label>
                <input type="email" id="forgot-email" placeholder="Your email">
            </div>
            <button id="forgot-submit-btn" class="btn btn-blue">Reset Password</button>
            <div class="form-footer">
                <p>Remember your password? <a href="#" id="back-to-login-link">Login here</a></p>
            </div>
        </div>
    </div>

    <!-- Terms and Conditions Modal -->
    <div class="terms-modal">
        <div class="terms-content">
            <button class="terms-close">&times;</button>
            <h2>Terms and Conditions</h2>
            <div class="terms-text">
                <p>Please read these terms and conditions carefully before using our service.</p>
                <h3>1. Terms</h3>
                <p>By accessing this website, you are agreeing to be bound by these terms of service, all applicable laws and regulations, and agree that you are responsible for compliance with any applicable local laws.</p>
                
                <h3>2. Use License</h3>
                <p>Permission is granted to temporarily use the materials on WorkRightTT's website for personal, non-commercial transitory viewing only.</p>
                
                <h3>3. Disclaimer</h3>
                <p>The materials on WorkRightTT's website are provided on an 'as is' basis. WorkRightTT makes no warranties, expressed or implied, and hereby disclaims and negates all other warranties including, without limitation, implied warranties or conditions of merchantability, fitness for a particular purpose, or non-infringement of intellectual property or other violation of rights.</p>
                
                <h3>4. Limitations</h3>
                <p>In no event shall WorkRightTT or its suppliers be liable for any damages (including, without limitation, damages for loss of data or profit, or due to business interruption) arising out of the use or inability to use the materials on WorkRightTT's website.</p>
                
                <h3>5. Accuracy of materials</h3>
                <p>The materials appearing on WorkRightTT's website could include technical, typographical, or photographic errors. WorkRightTT does not warrant that any of the materials on its website are accurate, complete or current.</p>
                
                <h3>6. Links</h3>
                <p>WorkRightTT has not reviewed all of the sites linked to its website and is not responsible for the contents of any such linked site. The inclusion of any link does not imply endorsement by WorkRightTT of the site. Use of any such linked website is at the user's own risk.</p>
                
                <h3>7. Modifications</h3>
                <p>WorkRightTT may revise these terms of service for its website at any time without notice. By using this website you are agreeing to be bound by the then current version of these terms of service.</p>
                
                <h3>8. Governing Law</h3>
                <p>These terms and conditions are governed by and construed in accordance with the laws of Trinidad and Tobago and you irrevocably submit to the exclusive jurisdiction of the courts in that location.</p>
            </div>
            <div class="terms-actions">
                <button class="btn" id="decline-terms">Decline</button>
                <button class="btn btn-blue" id="accept-terms">Accept</button>
            </div>
        </div>
    </div>

    <!-- Job Details Modal -->
    <div class="job-details-modal">
        <div class="job-details-content">
            <button class="job-details-close">&times;</button>
            <div class="job-details-header">
                <h2 id="detail-job-title">Job Title</h2>
                <div class="job-meta-row">
                    <div class="job-meta-item">
                        <i class="fas fa-building"></i>
                        <span id="detail-company">Company Name</span>
                    </div>
                    <div class="job-meta-item">
                        <i class="fas fa-map-marker-alt"></i>
                        <span id="detail-location">Location</span>
                    </div>
                    <div class="job-meta-item">
                        <i class="fas fa-dollar-sign"></i>
                        <span id="detail-salary">Salary</span>
                    </div>
                </div>
                <div class="job-meta-row">
                    <div class="job-meta-item">
                        <i class="fas fa-briefcase"></i>
                        <span id="detail-employment-type">Employment Type</span>
                    </div>
                    <div class="job-meta-item">
                        <i class="fas fa-clock"></i>
                        <span id="detail-posted-date">Posted Date</span>
                    </div>
                </div>
            </div>
            
            <div class="job-details-section">
                <h3>Job Description</h3>
                <p id="detail-description">Job description goes here...</p>
            </div>
            
            <div class="job-details-section">
                <h3>Requirements</h3>
                <p id="detail-requirements">Requirements go here...</p>
            </div>
            
            <div class="job-details-section">
                <h3>Responsibilities</h3>
                <p id="detail-responsibilities">Responsibilities go here...</p>
            </div>
            
            <div class="job-details-section">
                <h3>Benefits</h3>
                <p id="detail-benefits">Benefits go here...</p>
            </div>
            
            <div class="job-details-company">
                <h3>About the Company</h3>
                <p id="detail-company-bio">Company bio goes here...</p>
            </div>
            
            <div class="form-actions">
                <button class="btn" id="detail-close-btn">Close</button>
                <button class="btn btn-blue" id="detail-apply-btn">Apply Now</button>
            </div>
        </div>
    </div>

    <!-- Company Modal -->
    <div class="company-modal">
        <div class="company-content">
            <button class="company-close">&times;</button>
            <div class="company-header">
                <div class="company-logo">
                    <img src="https://via.placeholder.com/80" alt="Company Logo" id="company-modal-logo">
                </div>
                <div class="company-info">
                    <h2 id="company-modal-name">Company Name</h2>
                    <p id="company-modal-industry">Industry</p>
                    <p id="company-modal-location"><i class="fas fa-map-marker-alt"></i> Location</p>
                </div>
            </div>
            
            <div class="company-bio">
                <h3>About Us</h3>
                <p id="company-modal-bio">Company bio goes here...</p>
            </div>
            
            <div class="company-contact">
                <h3>Contact Information</h3>
                <p><i class="fas fa-envelope"></i> <span id="company-modal-email">Email</span></p>
                <p><i class="fas fa-phone"></i> <span id="company-modal-phone">Phone</span></p>
            </div>
            
            <div class="company-jobs">
                <h3>Current Job Openings</h3>
                <div class="company-jobs-list" id="company-jobs-list">
                    <!-- Company jobs will be dynamically inserted here -->
                </div>
            </div>
        </div>
    </div>

    <!-- Application Modal -->
    <div class="application-modal">
        <div class="application-form">
            <button class="application-close">&times;</button>
            <h2>Apply for <span id="apply-job-title">Job Title</span></h2>
            <p>at <span id="apply-company-name">Company Name</span></p>
            
            <div class="form-group">
                <label for="applicant-name">Full Name</label>
                <input type="text" id="applicant-name" placeholder="Your full name">
            </div>
            
            <div class="form-group">
                <label for="applicant-email">Email</label>
                <input type="email" id="applicant-email" placeholder="Your email">
            </div>
            
            <div class="form-group">
                <label for="applicant-phone">Phone Number</label>
                <input type="tel" id="applicant-phone" placeholder="Your phone number">
            </div>
            
            <div class="form-group">
                <label>Resume</label>
                <div class="file-input-container">
                    <div class="file-input-button">Choose File</div>
                    <input type="file" class="file-input" id="application-resume" accept=".pdf,.doc,.docx">
                    <span class="file-name" id="application-resume-name">No file chosen</span>
                </div>
            </div>
            
            <div class="form-group">
                <label for="application-cover-letter">Cover Letter (Optional)</label>
                <textarea id="application-cover-letter" placeholder="Write a cover letter..."></textarea>
            </div>
            
            <div class="form-actions">
                <button class="btn" id="application-cancel-btn">Cancel</button>
                <button class="btn btn-blue" id="application-submit-btn">Submit Application</button>
            </div>
        </div>
    </div>

    <!-- User Dashboard Modal -->
    <div class="user-dashboard">
        <div class="user-dashboard-content">
            <button class="user-dashboard-close">&times;</button>
            <h2>Your Dashboard</h2>
            
            <div class="user-dashboard-body">
                <div class="user-profile-section">
                    <div class="profile-header">
                        <h3><i class="fas fa-user"></i> Profile Information</h3>
                        <button class="btn" id="edit-profile-btn">Edit Profile</button>
                    </div>
                    
                    <div class="profile-card">
                        <div class="profile-avatar">
                            <i class="fas fa-user"></i>
                        </div>
                        <div class="profile-details">
                            <div class="detail-row">
                                <div class="detail-label">
                                    <i class="fas fa-user"></i>
                                    <span>Name:</span>
                                </div>
                                <div class="detail-value" id="dashboard-user-name">John Doe</div>
                            </div>
                            <div class="detail-row">
                                <div class="detail-label">
                                    <i class="fas fa-envelope"></i>
                                    <span>Email:</span>
                                </div>
                                <div class="detail-value" id="dashboard-user-email">john.doe@example.com</div>
                            </div>
                            <div class="detail-row">
                                <div class="detail-label">
                                    <i class="fas fa-phone"></i>
                                    <span>Phone:</span>
                                </div>
                                <div class="detail-value" id="dashboard-user-phone">+1 (868) 123-4567</div>
                            </div>
                            <div class="detail-row">
                                <div class="detail-label">
                                    <i class="fas fa-birthday-cake"></i>
                                    <span>Age:</span>
                                </div>
                                <div class="detail-value" id="dashboard-user-age">30</div>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="user-resume-section">
                    <h3><i class="fas fa-file-alt"></i> Your Resumes</h3>
                    <div class="user-profile-info">
                        <p>Primary Resume: <span id="primary-resume-name">resume.pdf</span> <button class="btn">Change</button></p>
                        <p>Secondary Resume: <span id="secondary-resume-name">None</span> <button class="btn">Upload</button></p>
                        <button class="btn">Manage Resumes</button>
                    </div>
                </div>
                
                <div class="user-saved-jobs">
                    <h3><i class="fas fa-bookmark"></i> Saved Jobs</h3>
                    <div id="saved-jobs-list">
                        <!-- Saved jobs will be dynamically inserted here -->
                        <p>No saved jobs yet.</p>
                    </div>
                </div>
                
                <div class="user-applied-jobs">
                    <h3><i class="fas fa-briefcase"></i> Applied Jobs</h3>
                    <div id="applied-jobs-list">
                        <!-- Applied jobs will be dynamically inserted here -->
                        <p>You haven't applied to any jobs yet.</p>
                    </div>
                </div>
                
                <div class="user-subscription-section">
                    <h3><i class="fas fa-bell"></i> Job Alerts</h3>
                    <div class="user-profile-info">
                        <p>Email notifications: <span id="subscription-status">Active</span> <button class="btn">Manage</button></p>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Admin Modals -->
    <!-- Add Job Modal -->
    <div class="admin-panel" id="add-job-modal">
        <div class="admin-form">
            <button class="admin-close">&times;</button>
            <h2>Add New Job</h2>
            
            <div class="form-group">
                <label for="job-title">Job Title</label>
                <input type="text" id="job-title" placeholder="Enter job title">
            </div>
            
            <div class="form-group">
                <label for="job-company">Company Name</label>
                <input type="text" id="job-company" placeholder="Enter company name">
            </div>
            
            <div class="form-group">
                <label for="job-location">Location</label>
                <input type="text" id="job-location" placeholder="Enter job location">
            </div>
            
            <div class="form-group">
                <label for="job-location-type">Work Location Type</label>
                <select id="job-location-type">
                    <option value="onsite">On Site</option>
                    <option value="hybrid">Hybrid</option>
                    <option value="remote">Remote</option>
                    <option value="wfh">Work from Home</option>
                </select>
            </div>
            
            <div class="form-group">
                <label for="job-latitude">Latitude</label>
                <input type="number" id="job-latitude" step="any" placeholder="e.g. 10.6543">
            </div>
            
            <div class="form-group">
                <label for="job-longitude">Longitude</label>
                <input type="number" id="job-longitude" step="any" placeholder="e.g. -61.3887">
            </div>
            
            <div class="form-group">
                <label for="job-industry">Industry</label>
                <select id="job-industry">
                    <option value="agriculture">Agriculture</option>
                    <option value="construction">Construction</option>
                    <option value="education">Education</option>
                    <option value="energy">Energy</option>
                    <option value="finance">Finance</option>
                    <option value="healthcare">Healthcare</option>
                    <option value="hospitality">Hospitality</option>
                    <option value="it">Information Technology</option>
                    <option value="manufacturing">Manufacturing</option>
                    <option value="mining">Mining</option>
                    <option value="other">Other</option>
                    <option value="retail">Retail</option>
                    <option value="transport">Transport</option>
                </select>
            </div>
            
            <div class="form-group">
                <label for="job-region">Region</label>
                <select id="job-region">
                    <option value="north">North</option>
                    <option value="central">Central</option>
                    <option value="south">South</option>
                    <option value="tobago">Tobago</option>
                </select>
            </div>
            
            <div class="form-group">
                <label for="job-salary-type">Salary Type</label>
                <select id="job-salary-type">
                    <option value="range">Range</option>
                    <option value="flat">Flat Rate</option>
                    <option value="undisclosed">Undisclosed</option>
                </select>
            </div>
            
            <div class="form-group" id="salary-range-group">
                <label for="job-salary-min">Salary Range (Min - Max TTD)</label>
                <div class="form-row">
                    <input type="number" id="job-salary-min" placeholder="Min">
                    <span>-</span>
                    <input type="number" id="job-salary-max" placeholder="Max">
                </div>
            </div>
            
            <div class="form-group" id="salary-flat-group" style="display: none;">
                <label for="job-salary-flat">Flat Salary (TTD)</label>
                <input type="number" id="job-salary-flat" placeholder="Flat salary">
            </div>
            
            <div class="form-group">
                <label for="job-salary-period">Salary Period</label>
                <select id="job-salary-period">
                    <option value="month">Per Month</option>
                    <option value="week">Per Week</option>
                    <option value="day">Per Day</option>
                    <option value="hour">Per Hour</option>
                </select>
            </div>
            
            <div class="form-group">
                <label for="job-employment-type">Employment Type</label>
                <select id="job-employment-type">
                    <option value="full-time">Full-time</option>
                    <option value="part-time">Part-time</option>
                    <option value="contract">Contract</option>
                    <option value="temporary">Temporary</option>
                    <option value="internship">Internship</option>
                </select>
            </div>
            
            <div class="form-group">
                <label for="job-certifications">Required Certifications (comma separated)</label>
                <input type="text" id="job-certifications" placeholder="e.g. OSHA, First Aid, Welding Certification">
            </div>
            
            <div class="form-group">
                <label for="job-description">Job Description</label>
                <textarea id="job-description" placeholder="Enter job description"></textarea>
            </div>
            
            <div class="form-group">
                <label for="job-requirements">Requirements</label>
                <textarea id="job-requirements" placeholder="Enter job requirements"></textarea>
            </div>
            
            <div class="form-group">
                <label for="job-responsibilities">Responsibilities (Optional)</label>
                <textarea id="job-responsibilities" placeholder="Enter job responsibilities"></textarea>
            </div>
            
            <div class="form-group">
                <label for="job-benefits">Benefits (Optional)</label>
                <textarea id="job-benefits" placeholder="Enter job benefits"></textarea>
            </div>
            
            <div class="form-group">
                <label for="job-deadline">Application Deadline</label>
                <input type="date" id="job-deadline">
            </div>
            
            <div class="form-group">
                <label for="job-contact-email">Contact Email</label>
                <input type="email" id="job-contact-email" placeholder="Email for applications">
            </div>
            
            <div class="form-group">
                <label for="job-verified">
                    <input type="checkbox" id="job-verified">
                    Verified Job
                </label>
            </div>
            
            <div class="form-group">
                <label for="job-urgent">
                    <input type="checkbox" id="job-urgent">
                    Urgent Hiring
                </label>
            </div>
            
            <div class="form-group">
                <label for="job-pinned">
                    <input type="checkbox" id="job-pinned">
                    Pinned Job
                </label>
            </div>
            
            <button id="save-job-btn" class="btn btn-blue">Save Job</button>
            <button class="btn" id="cancel-job-btn">Cancel</button>
        </div>
    </div>


<!-- Edit Jobs Modal -->
<div class="admin-panel" id="edit-jobs-modal">
    <div class="admin-form">
        <button class="admin-close">&times;</button>
        <h2>Edit Jobs</h2>
        
        <div class="admin-search-container">
            <div class="admin-search-bar">
                <select id="job-search-type">
                    <option value="title">Title</option>
                    <option value="company">Company</option>
                    <option value="location">Location</option>
                </select>
                <input type="text" id="job-search-input" placeholder="Search jobs...">
                <button id="job-search-btn" class="btn">Search</button>
            </div>
            
            <div class="admin-search-results" id="job-search-results">
                <!-- Job search results will be displayed here -->
                <div class="empty-message">Search for jobs to edit</div>
            </div>
        </div>
        
        <div id="job-edit-form" style="display: none;">
            <h3>Edit Job</h3>
            
            <div class="form-group">
                <label for="edit-job-title">Job Title</label>
                <input type="text" id="edit-job-title" placeholder="Enter job title">
            </div>
            
            <div class="form-group">
                <label for="edit-job-company">Company Name</label>
                <input type="text" id="edit-job-company" placeholder="Enter company name">
            </div>
            
            <!-- Include all other job fields similar to the add job form -->
            
            <div class="form-actions">
                <button id="update-job-btn" class="btn btn-blue">Update Job</button>
                <button id="delete-job-btn" class="btn btn-red">Delete Job</button>
                <button id="cancel-edit-btn" class="btn">Cancel</button>
            </div>
        </div>
    </div>
</div>

    <!-- Manage Companies Modal -->
    <div class="admin-panel" id="manage-companies-modal">
        <div class="admin-form">
            <button class="admin-close">&times;</button>
            <h2>Manage Companies</h2>
            
            <div class="admin-search-container">
                <div class="admin-search-bar">
                    <select id="company-search-type">
                        <option value="name">Name</option>
                        <option value="industry">Industry</option>
                    </select>
                    <input type="text" id="company-search-input" placeholder="Search companies...">
                    <button id="company-search-btn" class="btn">Search</button>
                </div>
                
                <div class="admin-search-results" id="company-search-results">
                    <!-- Company search results will be displayed here -->
                </div>
            </div>
            
            <h3>Add/Edit Company</h3>
            
            <div class="form-group">
                <label for="company-name">Company Name</label>
                <input type="text" id="company-name" placeholder="Enter company name">
            </div>
            
            <div class="form-group">
                <label for="company-industry">Industry</label>
                <select id="company-industry">
                    <option value="agriculture">Agriculture</option>
                    <option value="construction">Construction</option>
                    <option value="education">Education</option>
                    <option value="energy">Energy</option>
                    <option value="finance">Finance</option>
                    <option value="healthcare">Healthcare</option>
                    <option value="hospitality">Hospitality</option>
                    <option value="it">Information Technology</option>
                    <option value="manufacturing">Manufacturing</option>
                    <option value="mining">Mining</option>
                    <option value="other">Other</option>
                    <option value="retail">Retail</option>
                    <option value="transport">Transport</option>
                </select>
            </div>
            
            <div class="form-group">
                <label for="company-location">Location</label>
                <input type="text" id="company-location" placeholder="Enter company location">
            </div>
            
            <div class="form-group">
                <label for="company-email">Email</label>
                <input type="email" id="company-email" placeholder="Enter company email">
            </div>
            
            <div class="form-group">
                <label for="company-phone">Phone Number</label>
                <input type="tel" id="company-phone" placeholder="Enter company phone number">
            </div>
            
            <div class="form-group">
                <label for="company-bio">Company Bio</label>
                <textarea id="company-bio" placeholder="Enter company bio"></textarea>
            </div>
            
            <div class="form-group">
                <label>Company Logo</label>
                <div class="file-input-container">
                    <div class="file-input-button">Choose Logo</div>
                    <input type="file" class="file-input" id="company-logo" accept="image/*">
                    <span class="file-name" id="company-logo-name">No file chosen</span>
                </div>
            </div>
            
            <div class="form-group">
                <label for="company-verified">
                    <input type="checkbox" id="company-verified">
                    Verified Company
                </label>
            </div>
            
            <div class="form-actions">
                <button id="save-company-btn" class="btn btn-blue">Save Company</button>
                <button id="delete-company-btn" class="btn btn-red">Delete Company</button>
                <button id="new-company-btn" class="btn">New Company</button>
            </div>
        </div>
    </div>

    <!-- Manage Ads Modal -->
    <div class="admin-panel" id="manage-ads-modal">
        <div class="admin-form">
            <button class="admin-close">&times;</button>
            <h2>Manage Advertisements</h2>
            
            <div class="form-group">
                <label for="ad-rotation-time">Rotation Time (seconds)</label>
                <input type="number" id="ad-rotation-time" value="60" min="10">
            </div>
            
            <h3>Current Ads</h3>
            <div id="current-ads-list">
                <!-- Current ads will be displayed here -->
            </div>
            
            <h3>Upload New Ad</h3>
            
            <div class="form-group">
                <label>Ad Image</label>
                <div class="file-input-container">
                    <div class="file-input-button">Choose Image</div>
                    <input type="file" class="file-input" id="ad-image" accept="image/*">
                    <span class="file-name" id="ad-image-name">No file chosen</span>
                </div>
            </div>
            
            <div class="form-group">
                <label for="ad-link">Ad Link URL</label>
                <input type="url" id="ad-link" placeholder="https://example.com">
            </div>
            
            <button id="add-ad-btn" class="btn btn-blue">Add Advertisement</button>
            <button class="btn" id="close-ads-btn">Close</button>
        </div>
    </div>

    <!-- Admin Dashboard Modal -->
    <div class="admin-panel" id="admin-dashboard-modal">
        <div class="admin-dashboard-content">
            <button class="admin-dashboard-close">&times;</button>
            <h2>Admin Dashboard</h2>
            
            <div class="dashboard-stats">
                <div class="stat-card">
                    <h3>Total Jobs</h3>
                    <p id="total-jobs">0</p>
                </div>
                <div class="stat-card">
                    <h3>Total Applications</h3>
                    <p id="total-applications">0</p>
                </div>
                <div class="stat-card">
                    <h3>Total Users</h3>
                    <p id="total-users">0</p>
                </div>
                <div class="stat-card">
                    <h3>Total Resumes</h3>
                    <p id="total-resumes">0</p>
                </div>
            </div>
            
            <div class="dashboard-charts">
                <div class="chart-container">
                    <h3>Jobs by Industry</h3>
                    <canvas id="industry-chart"></canvas>
                </div>
                <div class="chart-container">
                    <h3>Applications Over Time</h3>
                    <canvas id="applications-chart"></canvas>
                </div>
            </div>
        </div>
    </div>

    <!-- Toast Notification -->
    <div class="toast" id="toast"></div>

    <!-- Firebase SDK -->
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-auth-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-storage-compat.js"></script>
    
    <!-- Leaflet JS -->
    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
    
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <script>
        // Firebase configuration
        const firebaseConfig = {
 apiKey: "AIzaSyBcsdFsOfK_rVUY7A4GAxPe0HEiUMt5wbc",

  authDomain: "we2345-f2d3a.firebaseapp.com",

  databaseURL: "https://we2345-f2d3a-default-rtdb.europe-west1.firebasedatabase.app",

  projectId: "we2345-f2d3a",

  storageBucket: "we2345-f2d3a.firebasestorage.app",

  messagingSenderId: "175043273488",

  appId: "1:175043273488:web:73517a55f8329c53993b95"

};
        // Initialize Firebase
        firebase.initializeApp(firebaseConfig);
        const db = firebase.firestore();
        const auth = firebase.auth();
        const storage = firebase.storage();

        // Initialize map
        let map = L.map('job-map').setView([10.6918, -61.2225], 10); // Centered on Trinidad

        // Add base layer
        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
        }).addTo(map);

        // Add markers for jobs (will be populated from Firestore)
        let jobMarkers = [];

        // DOM Elements
        const mobileMenuBtn = document.querySelector('.mobile-menu-btn');
        const nav = document.querySelector('nav ul');
        const loginBtn = document.getElementById('login-btn');
        const userLoginModal = document.querySelector('.user-login-modal');
        const userLoginClose = document.querySelector('.user-login-close');
        const registerLink = document.getElementById('register-link');
        const userRegisterModal = document.querySelector('.user-register-modal');
        const userRegisterClose = document.querySelector('.user-register-close');
        const loginLink = document.getElementById('login-link');
        const forgotPasswordLink = document.getElementById('forgot-password-link');
        const forgotPasswordModal = document.querySelector('.forgot-password-modal');
        const forgotPasswordClose = document.querySelector('.forgot-password-close');
        const backToLoginLink = document.getElementById('back-to-login-link');
        const termsLink = document.getElementById('terms-link');
        const termsModal = document.querySelector('.terms-modal');
        const termsClose = document.querySelector('.terms-close');
        const declineTerms = document.getElementById('decline-terms');
        const acceptTerms = document.getElementById('accept-terms');
        const darkModeToggle = document.querySelector('.dark-mode-toggle');
        const floatingControlsToggle = document.querySelector('.floating-controls-main-toggle');
        const floatingControlsContainer = document.querySelector('.floating-controls-container');
        const accessibilityToggle = document.querySelector('.accessibility-toggle');
        const languageToggle = document.querySelector('.language-toggle');
        const jobDetailsModal = document.querySelector('.job-details-modal');
        const jobDetailsClose = document.querySelector('.job-details-close');
        const detailCloseBtn = document.getElementById('detail-close-btn');
        const detailApplyBtn = document.getElementById('detail-apply-btn');
        const companyModal = document.querySelector('.company-modal');
        const companyClose = document.querySelector('.company-close');
        const applicationModal = document.querySelector('.application-modal');
        const applicationClose = document.querySelector('.application-close');
        const applicationCancelBtn = document.getElementById('application-cancel-btn');
        const applicationSubmitBtn = document.getElementById('application-submit-btn');
        const userDashboard = document.querySelector('.user-dashboard');
        const userDashboardClose = document.querySelector('.user-dashboard-close');
        const editProfileBtn = document.getElementById('edit-profile-btn');
        const toggleAdvancedFiltersBtn = document.getElementById('toggle-advanced-filters-btn');
        const advancedFilters = document.getElementById('advanced-filters');
        const toggleLocationFiltersBtn = document.getElementById('toggle-location-filters-btn');
        const locationFilters = document.getElementById('location-filters');
        const useMyLocationBtn = document.getElementById('use-my-location-btn');
        const locationStatus = document.getElementById('location-status');
        const searchJobsBtn = document.getElementById('search-jobs-btn');
        const resetSearchBtn = document.getElementById('reset-search-btn');
        const gridStyleBtns = document.querySelectorAll('.grid-style-btn');
        const jobsContainer = document.getElementById('jobs-container');
        const pageBtns = document.querySelectorAll('.page-btn');
        const goToPageInput = document.getElementById('go-to-page');
        const goToPageBtn = document.getElementById('go-to-page-btn');
        const clearComparisonBtn = document.getElementById('clear-comparison-btn');
        const comparisonCount = document.getElementById('comparison-count');
        const comparisonContainer = document.getElementById('comparison-container');
        const adSlides = document.querySelectorAll('.ad-slide');
        const adNavPrev = document.querySelector('.ad-nav.prev');
        const adNavNext = document.querySelector('.ad-nav.next');
        const adminControls = document.getElementById('admin-controls');
        const addJobBtn = document.getElementById('add-job-btn');
        const addJobModal = document.getElementById('add-job-modal');
        const adminCloseBtns = document.querySelectorAll('.admin-close');
        const manageCompaniesBtn = document.getElementById('manage-companies-btn');
        const manageCompaniesModal = document.getElementById('manage-companies-modal');
        const manageAdsBtn = document.getElementById('manage-ads-btn');
        const manageAdsModal = document.getElementById('manage-ads-modal');
        const dashboardBtn = document.getElementById('dashboard-btn');
        const adminDashboardModal = document.getElementById('admin-dashboard-modal');
        const adminDashboardClose = document.querySelector('.admin-dashboard-close');
        const jobSalaryType = document.getElementById('job-salary-type');
        const salaryRangeGroup = document.getElementById('salary-range-group');
        const salaryFlatGroup = document.getElementById('salary-flat-group');
        const saveJobBtn = document.getElementById('save-job-btn');
        const cancelJobBtn = document.getElementById('cancel-job-btn');
        const toast = document.getElementById('toast');

        // State variables
        let currentUser = null;
        let isAdmin = false;
        let currentAdIndex = 0;
        let adInterval;
        let selectedJobsForComparison = [];
        let currentPage = 1;
        const jobsPerPage = 9;
        let allJobs = [];

        // Event Listeners
        mobileMenuBtn.addEventListener('click', () => {
            nav.classList.toggle('show');
        });

        loginBtn.addEventListener('click', (e) => {
            e.preventDefault();
            userLoginModal.classList.add('active');
        });

        userLoginClose.addEventListener('click', () => {
            userLoginModal.classList.remove('active');
        });

        registerLink.addEventListener('click', (e) => {
            e.preventDefault();
            userLoginModal.classList.remove('active');
            userRegisterModal.classList.add('active');
        });

        userRegisterClose.addEventListener('click', () => {
            userRegisterModal.classList.remove('active');
        });

        loginLink.addEventListener('click', (e) => {
            e.preventDefault();
            userRegisterModal.classList.remove('active');
            userLoginModal.classList.add('active');
        });

        forgotPasswordLink.addEventListener('click', (e) => {
            e.preventDefault();
            userLoginModal.classList.remove('active');
            forgotPasswordModal.classList.add('active');
        });

        forgotPasswordClose.addEventListener('click', () => {
            forgotPasswordModal.classList.remove('active');
        });

        backToLoginLink.addEventListener('click', (e) => {
            e.preventDefault();
            forgotPasswordModal.classList.remove('active');
            userLoginModal.classList.add('active');
        });

        termsLink.addEventListener('click', (e) => {
            e.preventDefault();
            userRegisterModal.classList.remove('active');
            termsModal.classList.add('active');
        });

        termsClose.addEventListener('click', () => {
            termsModal.classList.remove('active');
        });

        declineTerms.addEventListener('click', () => {
            termsModal.classList.remove('active');
            userRegisterModal.classList.add('active');
        });

        acceptTerms.addEventListener('click', () => {
            termsModal.classList.remove('active');
            userRegisterModal.classList.add('active');
        });

        darkModeToggle.addEventListener('click', () => {
            document.documentElement.classList.toggle('dark-mode');
            const icon = darkModeToggle.querySelector('i');
            if (document.documentElement.classList.contains('dark-mode')) {
                icon.classList.remove('fa-moon');
                icon.classList.add('fa-sun');
            } else {
                icon.classList.remove('fa-sun');
                icon.classList.add('fa-moon');
            }
        });

        floatingControlsToggle.addEventListener('click', () => {
            floatingControlsContainer.classList.toggle('expanded');
        });

        accessibilityToggle.addEventListener('click', () => {
            document.documentElement.classList.toggle('high-contrast');
        });

        jobDetailsClose.addEventListener('click', () => {
            jobDetailsModal.classList.remove('active');
        });

        detailCloseBtn.addEventListener('click', () => {
            jobDetailsModal.classList.remove('active');
        });

        detailApplyBtn.addEventListener('click', () => {
            jobDetailsModal.classList.remove('active');
            applicationModal.classList.add('active');
        });

        companyClose.addEventListener('click', () => {
            companyModal.classList.remove('active');
        });

        applicationClose.addEventListener('click', () => {
            applicationModal.classList.remove('active');
        });

        applicationCancelBtn.addEventListener('click', () => {
            applicationModal.classList.remove('active');
        });

        userDashboardClose.addEventListener('click', () => {
            userDashboard.classList.remove('active');
        });

        editProfileBtn.addEventListener('click', () => {
            // Implement profile editing functionality
            showToast('Profile editing feature coming soon!', 'info');
        });

        toggleAdvancedFiltersBtn.addEventListener('click', () => {
            const isVisible = advancedFilters.style.display === 'block';
            advancedFilters.style.display = isVisible ? 'none' : 'block';
            toggleAdvancedFiltersBtn.innerHTML = isVisible ? 
                '<i class="fas fa-filter"></i> Show More Filters' : 
                '<i class="fas fa-filter"></i> Show Fewer Filters';
        });

        toggleLocationFiltersBtn.addEventListener('click', () => {
            const isVisible = locationFilters.style.display === 'block';
            locationFilters.style.display = isVisible ? 'none' : 'block';
            toggleLocationFiltersBtn.innerHTML = isVisible ? 
                '<i class="fas fa-map-marker-alt"></i> Show Location & Map Filters' : 
                '<i class="fas fa-map-marker-alt"></i> Hide Location & Map Filters';
        });

        useMyLocationBtn.addEventListener('click', () => {
            useMyLocationBtn.classList.add('loading');
            locationStatus.innerHTML = '<span class="location-loading"></span> Getting your location...';
            
            if (!navigator.geolocation) {
                locationStatus.textContent = 'Geolocation is not supported by your browser';
                useMyLocationBtn.classList.remove('loading');
                return;
            }
            
            navigator.geolocation.getCurrentPosition(
                (position) => {
                    const { latitude, longitude } = position.coords;
                    locationStatus.textContent = `Location found: ${latitude.toFixed(4)}, ${longitude.toFixed(4)}`;
                    useMyLocationBtn.classList.remove('loading');
                    
                    // Center map on user's location
                    map.setView([latitude, longitude], 13);
                    
                    // Add a marker for user's location
                    L.marker([latitude, longitude])
                        .addTo(map)
                        .bindPopup('Your location')
                        .openPopup();
                },
                (error) => {
                    locationStatus.textContent = 'Unable to retrieve your location';
                    useMyLocationBtn.classList.remove('loading');
                    console.error('Geolocation error:', error);
                }
            );
        });

        searchJobsBtn.addEventListener('click', () => {
            // Implement job search functionality
            filterJobs();
        });

        resetSearchBtn.addEventListener('click', () => {
            // Reset all search filters
            document.getElementById('job-title-search').value = '';
            document.getElementById('company-search').value = '';
            document.getElementById('certification-search').value = '';
            document.getElementById('industry-filter').value = '';
            document.getElementById('region-filter').value = '';
            document.getElementById('location-type-filter').value = '';
            document.getElementById('salary-range-filter').value = '';
            document.getElementById('salary-period-filter').value = '';
            document.getElementById('employment-type-filter').value = '';
            document.getElementById('posted-within-filter').value = '';
            document.getElementById('isochrone-filter').value = '0';
            
            // Reset map view
            map.setView([10.6918, -61.2225], 10);
            
            // Reload all jobs
            filterJobs();
        });

        gridStyleBtns.forEach(btn => {
            btn.addEventListener('click', () => {
                gridStyleBtns.forEach(b => b.classList.remove('active'));
                btn.classList.add('active');
                
                const view = btn.getAttribute('data-view');
                jobsContainer.className = `jobs-container ${view}-view`;
            });
        });

        pageBtns.forEach(btn => {
            btn.addEventListener('click', () => {
                if (btn.classList.contains('prev')) {
                    if (currentPage > 1) {
                        currentPage--;
                        renderJobs();
                    }
                } else if (btn.classList.contains('next')) {
                    if (currentPage < Math.ceil(allJobs.length / jobsPerPage)) {
                        currentPage++;
                        renderJobs();
                    }
                } else if (!btn.classList.contains('prev') && !btn.classList.contains('next')) {
                    currentPage = parseInt(btn.textContent);
                    renderJobs();
                }
                
                updatePagination();
            });
        });

        goToPageBtn.addEventListener('click', () => {
            const page = parseInt(goToPageInput.value);
            if (page && page > 0 && page <= Math.ceil(allJobs.length / jobsPerPage)) {
                currentPage = page;
                renderJobs();
                updatePagination();
            }
        });

        clearComparisonBtn.addEventListener('click', () => {
            selectedJobsForComparison = [];
            updateComparisonUI();
            
            // Uncheck all checkboxes
            document.querySelectorAll('.job-checkbox').forEach(checkbox => {
                checkbox.checked = false;
            });
        });

        adNavPrev.addEventListener('click', () => {
            showAd(currentAdIndex - 1);
        });

        adNavNext.addEventListener('click', () => {
            showAd(currentAdIndex + 1);
        });

        // Admin functionality
        addJobBtn.addEventListener('click', () => {
            addJobModal.classList.add('active');
        });

        adminCloseBtns.forEach(btn => {
            btn.addEventListener('click', () => {
                document.querySelectorAll('.admin-panel').forEach(panel => {
                    panel.classList.remove('active');
                });
            });
        });

        manageCompaniesBtn.addEventListener('click', () => {
            manageCompaniesModal.classList.add('active');
        });

        manageAdsBtn.addEventListener('click', () => {
            manageAdsModal.classList.add('active');
        });

        dashboardBtn.addEventListener('click', () => {
            adminDashboardModal.classList.add('active');
            loadDashboardData();
        });

        adminDashboardClose.addEventListener('click', () => {
            adminDashboardModal.classList.remove('active');
        });

        jobSalaryType.addEventListener('change', () => {
            const value = jobSalaryType.value;
            if (value === 'range') {
                salaryRangeGroup.style.display = 'block';
                salaryFlatGroup.style.display = 'none';
            } else if (value === 'flat') {
                salaryRangeGroup.style.display = 'none';
                salaryFlatGroup.style.display = 'block';
            } else {
                salaryRangeGroup.style.display = 'none';
                salaryFlatGroup.style.display = 'none';
            }
        });

        saveJobBtn.addEventListener('click', () => {
            saveJob();
        });

        cancelJobBtn.addEventListener('click', () => {
            addJobModal.classList.remove('active');
        });

// Edit Jobs functionality
const editJobsBtn = document.getElementById('edit-jobs-btn');
const editJobsModal = document.getElementById('edit-jobs-modal');
const jobSearchBtn = document.getElementById('job-search-btn');
const jobSearchResults = document.getElementById('job-search-results');
const jobEditForm = document.getElementById('job-edit-form');
const updateJobBtn = document.getElementById('update-job-btn');
const deleteJobBtn = document.getElementById('delete-job-btn');
const cancelEditBtn = document.getElementById('cancel-edit-btn');

// Open edit jobs modal
editJobsBtn.addEventListener('click', () => {
    editJobsModal.classList.add('active');
});

// Search for jobs to edit
jobSearchBtn.addEventListener('click', () => {
    const searchType = document.getElementById('job-search-type').value;
    const searchValue = document.getElementById('job-search-input').value.toLowerCase();
    
    if (!searchValue) {
        jobSearchResults.innerHTML = '<div class="empty-message">Please enter a search term</div>';
        return;
    }
    
    // Filter jobs based on search criteria
    const filteredJobs = allJobs.filter(job => {
        if (searchType === 'title') {
            return job.title.toLowerCase().includes(searchValue);
        } else if (searchType === 'company') {
            return job.company.name.toLowerCase().includes(searchValue);
        } else if (searchType === 'location') {
            return job.location.toLowerCase().includes(searchValue);
        }
        return false;
    });
    
    // Display search results
    if (filteredJobs.length === 0) {
        jobSearchResults.innerHTML = '<div class="empty-message">No jobs found</div>';
        return;
    }
    
    jobSearchResults.innerHTML = '';
    filteredJobs.forEach(job => {
        const resultItem = document.createElement('div');
        resultItem.className = 'admin-job-result';
        resultItem.innerHTML = `
            <h4>${job.title}</h4>
            <p>${job.company.name} - ${job.location}</p>
            <button class="btn edit-job-btn" data-id="${job.id}">Edit</button>
        `;
        jobSearchResults.appendChild(resultItem);
    });
    
    // Add event listeners to edit buttons
    document.querySelectorAll('.edit-job-btn').forEach(btn => {
        btn.addEventListener('click', () => {
            const jobId = btn.getAttribute('data-id');
            loadJobForEditing(jobId);
        });
    });
});

// Load job data for editing
function loadJobForEditing(jobId) {
    const job = allJobs.find(j => j.id === jobId);
    if (!job) return;
    
    // Populate the edit form with job data
    document.getElementById('edit-job-title').value = job.title;
    document.getElementById('edit-job-company').value = job.company.name;
    // Populate all other fields similarly
    
    // Store the job ID for reference
    jobEditForm.setAttribute('data-job-id', jobId);
    
    // Show the edit form
    jobEditForm.style.display = 'block';
}

// Update job
updateJobBtn.addEventListener('click', () => {
    const jobId = jobEditForm.getAttribute('data-job-id');
    if (!jobId) return;
    
    // Get updated values from form
    const updatedData = {
        title: document.getElementById('edit-job-title').value,
        company: {
            name: document.getElementById('edit-job-company').value,
            id: '' // This should be updated with actual company ID
        },
        // Include all other fields
    };
    
    // Update job in Firestore
    db.collection('jobs').doc(jobId).update(updatedData)
        .then(() => {
            showToast('Job updated successfully!', 'success');
            
            // Update the job in the local array
            const index = allJobs.findIndex(j => j.id === jobId);
            if (index !== -1) {
                allJobs[index] = { ...allJobs[index], ...updatedData };
            }
            
            // Refresh UI
            renderJobs();
            updateMapMarkers();
            
            // Hide the edit form
            jobEditForm.style.display = 'none';
        })
        .catch((error) => {
            showToast('Error updating job: ' + error.message, 'error');
            console.error('Error updating job: ', error);
        });
});

// Delete job
deleteJobBtn.addEventListener('click', () => {
    const jobId = jobEditForm.getAttribute('data-job-id');
    if (!jobId) return;
    
    if (!confirm('Are you sure you want to delete this job?')) return;
    
    // Delete job from Firestore
    db.collection('jobs').doc(jobId).delete()
        .then(() => {
            showToast('Job deleted successfully!', 'success');
            
            // Remove the job from the local array
            allJobs = allJobs.filter(j => j.id !== jobId);
            
            // Refresh UI
            renderJobs();
            updateMapMarkers();
            updatePagination();
            
            // Hide the edit form
            jobEditForm.style.display = 'none';
        })
        .catch((error) => {
            showToast('Error deleting job: ' + error.message, 'error');
            console.error('Error deleting job: ', error);
        });
});

// Cancel editing
cancelEditBtn.addEventListener('click', () => {
    jobEditForm.style.display = 'none';
});

        // Functions
        function showAd(index) {
            // Handle wrapping around
            if (index < 0) index = adSlides.length - 1;
            if (index >= adSlides.length) index = 0;
            
            // Hide all slides
            adSlides.forEach(slide => slide.classList.remove('active'));
            
            // Show the selected slide
            adSlides[index].classList.add('active');
            currentAdIndex = index;
        }

        function startAdRotation() {
            clearInterval(adInterval);
            const rotationTime = 60000; // 60 seconds
            adInterval = setInterval(() => {
                showAd(currentAdIndex + 1);
            }, rotationTime);
        }

        function filterJobs() {
            // Get filter values
            const title = document.getElementById('job-title-search').value.toLowerCase();
            const company = document.getElementById('company-search').value.toLowerCase();
            const certification = document.getElementById('certification-search').value.toLowerCase();
            const industry = document.getElementById('industry-filter').value;
            const region = document.getElementById('region-filter').value;
            const locationType = document.getElementById('location-type-filter').value;
            const salaryRange = document.getElementById('salary-range-filter').value;
            const salaryPeriod = document.getElementById('salary-period-filter').value;
            const employmentType = document.getElementById('employment-type-filter').value;
            const postedWithin = document.getElementById('posted-within-filter').value;
            
            // Filter jobs based on criteria
            const filteredJobs = allJobs.filter(job => {
                // Title filter
                if (title && !job.title.toLowerCase().includes(title)) return false;
                
                // Company filter
                if (company && !job.company.name.toLowerCase().includes(company)) return false;
                
                // Certification filter
                if (certification && job.certifications) {
                    const certs = job.certifications.map(c => c.toLowerCase());
                    if (!certs.some(c => c.includes(certification))) return false;
                }
                
                // Industry filter
                if (industry && job.industry !== industry) return false;
                
                // Region filter
                if (region && job.region !== region) return false;
                
                // Location type filter
                if (locationType && job.locationType !== locationType) return false;
                
                // Salary range filter
                if (salaryRange && job.salary) {
                    if (salaryRange === '0-3000' && (job.salary.max > 3000 || job.salary.type === 'undisclosed')) return false;
                    if (salaryRange === '3000-6000' && (job.salary.max <= 3000 || job.salary.max > 6000)) return false;
                    if (salaryRange === '6000-10000' && (job.salary.max <= 6000 || job.salary.max > 10000)) return false;
                    if (salaryRange === '10000+' && job.salary.max <= 10000) return false;
                }
                
                // Salary period filter
                if (salaryPeriod && job.salary && job.salary.period !== salaryPeriod) return false;
                
                // Employment type filter
                if (employmentType && job.employmentType !== employmentType) return false;
                
                // Posted within filter
                if (postedWithin) {
                    const days = parseInt(postedWithin);
                    const postedDate = new Date(job.postedDate);
                    const now = new Date();
                    const diffTime = Math.abs(now - postedDate);
                    const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
                    if (diffDays > days) return false;
                }
                
                return true;
            });
            
            // Update jobs display
            allJobs = filteredJobs;
            currentPage = 1;
            renderJobs();
            updatePagination();
            updateMapMarkers();
        }

        function renderJobs() {
            // Clear current jobs
            jobsContainer.innerHTML = '';
            
            // Calculate pagination
            const startIndex = (currentPage - 1) * jobsPerPage;
            const endIndex = startIndex + jobsPerPage;
            const jobsToShow = allJobs.slice(startIndex, endIndex);
            
            if (jobsToShow.length === 0) {
                jobsContainer.innerHTML = '<div class="empty-message"><p>No jobs found matching your criteria.</p></div>';
                return;
            }
            
            // Create job cards
            jobsToShow.forEach(job => {
                const jobCard = createJobCard(job);
                jobsContainer.appendChild(jobCard);
            });
        }

        function createJobCard(job) {
            const card = document.createElement('div');
            card.className = 'job-card';
            card.dataset.id = job.id;
            
            // Add pinned badge if applicable
            if (job.pinned) {
                const pinnedBadge = document.createElement('div');
                pinnedBadge.className = 'pinned-badge';
                pinnedBadge.textContent = 'Pinned';
                card.appendChild(pinnedBadge);
            }
            
            // Add checkbox for comparison
            const checkbox = document.createElement('input');
            checkbox.type = 'checkbox';
            checkbox.className = 'job-checkbox';
            checkbox.addEventListener('change', (e) => {
                if (e.target.checked) {
                    if (selectedJobsForComparison.length >= 5) {
                        showToast('You can only compare up to 5 jobs', 'error');
                        e.target.checked = false;
                        return;
                    }
                    selectedJobsForComparison.push(job);
                } else {
                    selectedJobsForComparison = selectedJobsForComparison.filter(j => j.id !== job.id);
                }
                updateComparisonUI();
            });
            card.appendChild(checkbox);
            
            // Add verified badge if applicable
            if (job.verified) {
                const verifiedBadge = document.createElement('div');
                verifiedBadge.className = 'verified-badge';
                verifiedBadge.innerHTML = '<i class="fas fa-check-circle"></i>';
                card.appendChild(verifiedBadge);
            }
            
            // Add title
            const title = document.createElement('h3');
            title.textContent = job.title;
            card.appendChild(title);
            
            // Add company
            const company = document.createElement('div');
            company.className = 'company';
            company.innerHTML = job.company.name;
            if (job.company.verified) {
                company.innerHTML += ' <span class="company-verified"><i class="fas fa-check-circle"></i></span>';
            }
            company.addEventListener('click', () => {
                showCompanyModal(job.company);
            });
            card.appendChild(company);
            
            // Add location
            const location = document.createElement('div');
            location.className = 'location';
            location.innerHTML = `<i class="fas fa-map-marker-alt"></i> ${job.location} • ${formatLocationType(job.locationType)}`;
            location.addEventListener('click', () => {
                // Center map on this job
                map.setView([job.latitude, job.longitude], 13);
            });
            card.appendChild(location);
            
            // Add salary
            if (job.salary && job.salary.type !== 'undisclosed') {
                const salary = document.createElement('div');
                salary.className = 'salary';
                salary.textContent = formatSalary(job.salary);
                card.appendChild(salary);
            } else if (job.salary && job.salary.type === 'undisclosed') {
                const salary = document.createElement('div');
                salary.className = 'salary undisclosed';
                salary.textContent = 'Salary: Undisclosed';
                card.appendChild(salary);
            }
            
            // Add job meta (type and posted date)
            const jobMeta = document.createElement('div');
            jobMeta.className = 'job-meta';
            jobMeta.innerHTML = `
                <span>${formatEmploymentType(job.employmentType)}</span>
                <span>${formatPostedDate(job.postedDate)}</span>
            `;
            card.appendChild(jobMeta);
            
            // Add deadline if applicable
            if (job.deadline) {
                const deadline = document.createElement('div');
                deadline.className = 'deadline';
                deadline.innerHTML = `<i class="fas fa-clock"></i> Apply by ${formatDate(job.deadline)}`;
                if (job.urgent) {
                    deadline.innerHTML += ` <span class="urgent-badge">Urgent</span>`;
                }
                card.appendChild(deadline);
            }
            
            // Add certifications if available
            if (job.certifications && job.certifications.length > 0) {
                const certsContainer = document.createElement('div');
                certsContainer.className = 'certifications';
                job.certifications.forEach(cert => {
                    const badge = document.createElement('span');
                    badge.className = 'certification-badge';
                    badge.textContent = cert;
                    certsContainer.appendChild(badge);
                });
                card.appendChild(certsContainer);
            }
            
            // Add description
            const description = document.createElement('div');
            description.className = 'description';
            description.textContent = truncateText(job.description, 150);
            card.appendChild(description);
            
            // Add requirements
            const requirements = document.createElement('div');
            requirements.className = 'requirements';
            requirements.textContent = truncateText(job.requirements, 100);
            card.appendChild(requirements);
            
            // Add job actions
            const actions = document.createElement('div');
            actions.className = 'job-actions';
            
            const viewDetailsBtn = document.createElement('button');
            viewDetailsBtn.className = 'btn';
            viewDetailsBtn.innerHTML = '<i class="fas fa-info-circle"></i> Details';
            viewDetailsBtn.addEventListener('click', () => {
                showJobDetails(job);
            });
            actions.appendChild(viewDetailsBtn);
            
            const applyBtn = document.createElement('button');
            applyBtn.className = 'btn btn-blue';
            applyBtn.innerHTML = '<i class="fas fa-paper-plane"></i> Apply';
            applyBtn.addEventListener('click', () => {
                if (!currentUser) {
                    showToast('Please login to apply for jobs', 'error');
                    userLoginModal.classList.add('active');
                    return;
                }
                showApplicationModal(job);
            });
            actions.appendChild(applyBtn);
            
            // Add save button for logged in users
            if (currentUser) {
                const saveBtn = document.createElement('button');
                saveBtn.className = 'save-job-btn';
                saveBtn.innerHTML = '<i class="far fa-bookmark"></i>';
                saveBtn.addEventListener('click', () => {
                    toggleSaveJob(job, saveBtn);
                });
                actions.appendChild(saveBtn);
                
                // Check if job is already saved
                checkIfJobSaved(job, saveBtn);
            }
            
            card.appendChild(actions);
            
            return card;
        }

        function updatePagination() {
            const totalPages = Math.ceil(allJobs.length / jobsPerPage);
            const paginationContainer = document.querySelector('.pagination');
            
            // Clear existing buttons except prev and next
            const prevBtn = paginationContainer.querySelector('.prev');
            const nextBtn = paginationContainer.querySelector('.next');
            paginationContainer.innerHTML = '';
            paginationContainer.appendChild(prevBtn);
            
            // Add page buttons
            for (let i = 1; i <= totalPages; i++) {
                const pageBtn = document.createElement('button');
                pageBtn.className = 'page-btn';
                if (i === currentPage) pageBtn.classList.add('active');
                pageBtn.textContent = i;
                pageBtn.addEventListener('click', () => {
                    currentPage = i;
                    renderJobs();
                    updatePagination();
                });
                paginationContainer.appendChild(pageBtn);
            }
            
            paginationContainer.appendChild(nextBtn);
        }

        function updateComparisonUI() {
            comparisonCount.textContent = `${selectedJobsForComparison.length}/5 jobs selected`;
            
            // Clear comparison container
            comparisonContainer.innerHTML = '';
            
            if (selectedJobsForComparison.length === 0) {
                comparisonContainer.innerHTML = `
                    <div class="empty-message">
                        <p>No jobs selected for comparison. Select jobs using the checkboxes on job cards.</p>
                    </div>
                `;
                return;
            }
            
            // Add comparison jobs
            selectedJobsForComparison.forEach(job => {
                const comparisonJob = document.createElement('div');
                comparisonJob.className = 'comparison-job';
                comparisonJob.dataset.id = job.id;
                
                comparisonJob.innerHTML = `
                    <button class="remove-comparison">&times;</button>
                    <h3>${job.title}</h3>
                    <div class="company">${job.company.name}</div>
                    <div class="job-detail">
                        <strong>Location</strong>
                        <div>${job.location} • ${formatLocationType(job.locationType)}</div>
                    </div>
                    <div class="job-detail">
                        <strong>Salary</strong>
                        <div>${job.salary ? formatSalary(job.salary) : 'Not specified'}</div>
                    </div>
                    <div class="job-detail">
                        <strong>Employment Type</strong>
                        <div>${formatEmploymentType(job.employmentType)}</div>
                    </div>
                    <div class="job-detail">
                        <strong>Posted</strong>
                        <div>${formatPostedDate(job.postedDate)}</div>
                    </div>
                    <button class="btn btn-blue">View Details</button>
                `;
                
                comparisonJob.querySelector('.remove-comparison').addEventListener('click', () => {
                    selectedJobsForComparison = selectedJobsForComparison.filter(j => j.id !== job.id);
                    updateComparisonUI();
                    
                    // Uncheck the checkbox
                    const checkbox = document.querySelector(`.job-checkbox[data-id="${job.id}"]`);
                    if (checkbox) checkbox.checked = false;
                });
                
                comparisonJob.querySelector('.btn').addEventListener('click', () => {
                    showJobDetails(job);
                });
                
                comparisonContainer.appendChild(comparisonJob);
            });
        }

        function updateMapMarkers() {
            // Clear existing markers
            jobMarkers.forEach(marker => map.removeLayer(marker));
            jobMarkers = [];
            
            // Add markers for each job
            allJobs.forEach(job => {
                if (job.latitude && job.longitude) {
                    const marker = L.marker([job.latitude, job.longitude])
                        .addTo(map)
                        .bindPopup(`
                            <strong>${job.title}</strong><br>
                            ${job.company.name}<br>
                            ${job.location}<br>
                            <button onclick="showJobDetails('${job.id}')">View Details</button>
                        `);
                    
                    jobMarkers.push(marker);
                }
            });
        }

        function showJobDetails(job) {
            // If job is passed as ID, find the job object
            if (typeof job === 'string') {
                job = allJobs.find(j => j.id === job);
                if (!job) return;
            }
            
            // Populate job details
            document.getElementById('detail-job-title').textContent = job.title;
            document.getElementById('detail-company').textContent = job.company.name;
            document.getElementById('detail-location').textContent = job.location;
            document.getElementById('detail-salary').textContent = job.salary ? formatSalary(job.salary) : 'Not specified';
            document.getElementById('detail-employment-type').textContent = formatEmploymentType(job.employmentType);
            document.getElementById('detail-posted-date').textContent = formatPostedDate(job.postedDate);
            document.getElementById('detail-description').textContent = job.description;
            document.getElementById('detail-requirements').textContent = job.requirements;
            document.getElementById('detail-responsibilities').textContent = job.responsibilities || 'Not specified';
            document.getElementById('detail-benefits').textContent = job.benefits || 'Not specified';
            document.getElementById('detail-company-bio').textContent = job.company.bio || 'No company information available';
            
            // Show the modal
            jobDetailsModal.classList.add('active');
        }

        function showCompanyModal(company) {
            // Populate company details
            document.getElementById('company-modal-name').textContent = company.name;
            document.getElementById('company-modal-industry').textContent = formatIndustry(company.industry);
            document.getElementById('company-modal-location').textContent = company.location;
            document.getElementById('company-modal-email').textContent = company.email || 'Not provided';
            document.getElementById('company-modal-phone').textContent = company.phone || 'Not provided';
            document.getElementById('company-modal-bio').textContent = company.bio || 'No company information available';
            
            // Set company logo
            const logo = document.getElementById('company-modal-logo');
            if (company.logo) {
                logo.src = company.logo;
            } else {
                logo.src = 'https://via.placeholder.com/80';
            }
            
            // Load company jobs
            const jobsList = document.getElementById('company-jobs-list');
            jobsList.innerHTML = '';
            
            const companyJobs = allJobs.filter(job => job.company.id === company.id);
            if (companyJobs.length === 0) {
                jobsList.innerHTML = '<p>No current job openings</p>';
            } else {
                companyJobs.forEach(job => {
                    const jobCard = document.createElement('div');
                    jobCard.className = 'company-job-card';
                    jobCard.innerHTML = `
                        <h4>${job.title}</h4>
                        <p>${formatEmploymentType(job.employmentType)}</p>
                        <p>${job.location}</p>
                        <button class="btn">View Job</button>
                    `;
                    
                    jobCard.querySelector('.btn').addEventListener('click', () => {
                        companyModal.classList.remove('active');
                        showJobDetails(job);
                    });
                    
                    jobsList.appendChild(jobCard);
                });
            }
            
            // Show the modal
            companyModal.classList.add('active');
        }

        function showApplicationModal(job) {
            // Populate application form
            document.getElementById('apply-job-title').textContent = job.title;
            document.getElementById('apply-company-name').textContent = job.company.name;
            
            // Prefill user data if available
            if (currentUser) {
                document.getElementById('applicant-name').value = currentUser.displayName || '';
                document.getElementById('applicant-email').value = currentUser.email || '';
            }
            
            // Show the modal
            applicationModal.classList.add('active');
        }

        function toggleSaveJob(job, button) {
            // Implement save/unsave functionality
            const isSaved = button.classList.contains('saved');
            
            if (isSaved) {
                // Unsave job
                button.classList.remove('saved');
                button.innerHTML = '<i class="far fa-bookmark"></i>';
                showToast('Job removed from saved jobs', 'success');
            } else {
                // Save job
                button.classList.add('saved');
                button.innerHTML = '<i class="fas fa-bookmark"></i>';
                showToast('Job saved successfully', 'success');
            }
        }

        function checkIfJobSaved(job, button) {
            // Check if job is saved by user
            // This would typically check against a user's saved jobs in the database
            const isSaved = false; // Placeholder
            if (isSaved) {
                button.classList.add('saved');
                button.innerHTML = '<i class="fas fa-bookmark"></i>';
            }
        }

        function saveJob() {
            // Get form values
            const jobData = {
                title: document.getElementById('job-title').value,
                company: {
                    name: document.getElementById('job-company').value,
                    id: '' // This would typically be a company ID from the database
                },
                location: document.getElementById('job-location').value,
                locationType: document.getElementById('job-location-type').value,
                latitude: parseFloat(document.getElementById('job-latitude').value),
                longitude: parseFloat(document.getElementById('job-longitude').value),
                industry: document.getElementById('job-industry').value,
                region: document.getElementById('job-region').value,
                salary: {
                    type: document.getElementById('job-salary-type').value
                },
                employmentType: document.getElementById('job-employment-type').value,
                certifications: document.getElementById('job-certifications').value.split(',').map(c => c.trim()),
                description: document.getElementById('job-description').value,
                requirements: document.getElementById('job-requirements').value,
                responsibilities: document.getElementById('job-responsibilities').value,
                benefits: document.getElementById('job-benefits').value,
                deadline: document.getElementById('job-deadline').value,
                contactEmail: document.getElementById('job-contact-email').value,
                verified: document.getElementById('job-verified').checked,
                urgent: document.getElementById('job-urgent').checked,
                pinned: document.getElementById('job-pinned').checked,
                postedDate: new Date().toISOString()
            };
            
            // Handle salary data based on type
            if (jobData.salary.type === 'range') {
                jobData.salary.min = parseFloat(document.getElementById('job-salary-min').value);
                jobData.salary.max = parseFloat(document.getElementById('job-salary-max').value);
            } else if (jobData.salary.type === 'flat') {
                jobData.salary.amount = parseFloat(document.getElementById('job-salary-flat').value);
            }
            
            jobData.salary.period = document.getElementById('job-salary-period').value;
            
            // Save job to Firestore
            db.collection('jobs').add(jobData)
                .then((docRef) => {
                    showToast('Job posted successfully!', 'success');
                    addJobModal.classList.remove('active');
                    
                    // Add the new job to the local array
                    jobData.id = docRef.id;
                    allJobs.unshift(jobData);
                    
                    // Update UI
                    renderJobs();
                    updatePagination();
                    updateMapMarkers();
                })
                .catch((error) => {
                    showToast('Error posting job: ' + error.message, 'error');
                    console.error('Error adding job: ', error);
                });
        }

        function loadDashboardData() {
            // Load stats for admin dashboard
            Promise.all([
                db.collection('jobs').get(),
                db.collection('applications').get(),
                db.collection('users').get(),
                db.collection('resumes').get()
            ]).then(([jobsSnapshot, applicationsSnapshot, usersSnapshot, resumesSnapshot]) => {
                document.getElementById('total-jobs').textContent = jobsSnapshot.size;
                document.getElementById('total-applications').textContent = applicationsSnapshot.size;
                document.getElementById('total-users').textContent = usersSnapshot.size;
                document.getElementById('total-resumes').textContent = resumesSnapshot.size;
                
                // Generate industry chart
                const industryData = {};
                jobsSnapshot.forEach(doc => {
                    const industry = doc.data().industry;
                    industryData[industry] = (industryData[industry] || 0) + 1;
                });
                
                const industryChart = new Chart(document.getElementById('industry-chart'), {
                    type: 'pie',
                    data: {
                        labels: Object.keys(industryData),
                        datasets: [{
                            data: Object.values(industryData),
                            backgroundColor: [
                                '#FF6384', '#36A2EB', '#FFCE56', '#4BC0C0', '#9966FF', '#FF9F40',
                                '#FF6384', '#36A2EB', '#FFCE56', '#4BC0C0', '#9966FF', '#FF9F40'
                            ]
                        }]
                    }
                });
                
                // Generate applications chart (placeholder)
                const applicationsChart = new Chart(document.getElementById('applications-chart'), {
                    type: 'line',
                    data: {
                        labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun'],
                        datasets: [{
                            label: 'Applications',
                            data: [12, 19, 3, 5, 2, 3],
                            borderColor: '#36A2EB',
                            tension: 0.1
                        }]
                    }
                });
            });
        }

        function showToast(message, type = 'info') {
            toast.textContent = message;
            toast.className = `toast ${type}`;
            toast.classList.add('show');
            
            setTimeout(() => {
                toast.classList.remove('show');
            }, 3000);
        }

        // Utility functions
        function formatSalary(salary) {
            if (salary.type === 'undisclosed') return 'Salary: Undisclosed';
            if (salary.type === 'flat') return `Salary: $${salary.amount} ${formatSalaryPeriod(salary.period)}`;
            if (salary.type === 'range') return `Salary: $${salary.min} - $${salary.max} ${formatSalaryPeriod(salary.period)}`;
            return 'Salary: Not specified';
        }

        function formatSalaryPeriod(period) {
            switch (period) {
                case 'month': return 'per month';
                case 'week': return 'per week';
                case 'day': return 'per day';
                case 'hour': return 'per hour';
                default: return '';
            }
        }

        function formatEmploymentType(type) {
            switch (type) {
                case 'full-time': return 'Full-time';
                case 'part-time': return 'Part-time';
                case 'contract': return 'Contract';
                case 'temporary': return 'Temporary';
                case 'internship': return 'Internship';
                default: return type;
            }
        }

        function formatLocationType(type) {
            switch (type) {
                case 'onsite': return 'On Site';
                case 'hybrid': return 'Hybrid';
                case 'remote': return 'Remote';
                case 'wfh': return 'Work from Home';
                default: return type;
            }
        }

        function formatIndustry(industry) {
            return industry.charAt(0).toUpperCase() + industry.slice(1);
        }

        function formatPostedDate(dateString) {
            const date = new Date(dateString);
            const now = new Date();
            const diffTime = Math.abs(now - date);
            const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
            
            if (diffDays === 1) return '1 day ago';
            if (diffDays < 7) return `${diffDays} days ago`;
            if (diffDays < 30) return `${Math.ceil(diffDays / 7)} weeks ago`;
            return `${Math.ceil(diffDays / 30)} months ago`;
        }

        function formatDate(dateString) {
            const date = new Date(dateString);
            return date.toLocaleDateString('en-US', { year: 'numeric', month: 'long', day: 'numeric' });
        }

        function truncateText(text, maxLength) {
            if (text.length <= maxLength) return text;
            return text.substring(0, maxLength) + '...';
        }

        // Initialize the application
        function init() {
            // Start ad rotation
            startAdRotation();
            
            // Load jobs from Firestore
            db.collection('jobs').orderBy('postedDate', 'desc').get()
                .then((querySnapshot) => {
                    allJobs = [];
                    querySnapshot.forEach((doc) => {
                        const job = doc.data();
                        job.id = doc.id;
                        allJobs.push(job);
                    });
                    
                    renderJobs();
                    updatePagination();
                    updateMapMarkers();
                })
                .catch((error) => {
                    console.error('Error getting jobs: ', error);
                    showToast('Error loading jobs', 'error');
                });
            
            // Check if user is logged in
            auth.onAuthStateChanged((user) => {
                currentUser = user;
                
                if (user) {
                    // User is signed in
                    loginBtn.innerHTML = '<i class="fas fa-user"></i> Profile';
                    loginBtn.removeEventListener('click', null);
                    loginBtn.addEventListener('click', (e) => {
                        e.preventDefault();
                        userDashboard.classList.add('active');
                        loadUserDashboard();
                    });
                    
                    // Check if user is admin
                    db.collection('users').doc(user.uid).get()
                        .then((doc) => {
                            if (doc.exists && doc.data().isAdmin) {
                                isAdmin = true;
                                adminControls.style.display = 'block';
                            }
                        });
                } else {
                    // User is signed out
                    loginBtn.innerHTML = '<i class="fas fa-sign-in-alt"></i> Login';
                    loginBtn.removeEventListener('click', null);
                    loginBtn.addEventListener('click', (e) => {
                        e.preventDefault();
                        userLoginModal.classList.add('active');
                    });
                    
                    isAdmin = false;
                    adminControls.style.display = 'none';
                }
            });
            
            // Set up login form
            document.getElementById('login-submit-btn').addEventListener('click', () => {
                const email = document.getElementById('login-email').value;
                const password = document.getElementById('login-password').value;
                
                auth.signInWithEmailAndPassword(email, password)
                    .then((userCredential) => {
                        userLoginModal.classList.remove('active');
                        showToast('Login successful!', 'success');
                    })
                    .catch((error) => {
                        showToast('Login error: ' + error.message, 'error');
                    });
            });
            
            // Set up registration form
            document.getElementById('register-submit-btn').addEventListener('click', () => {
                const name = document.getElementById('register-name').value;
                const email = document.getElementById('register-email').value;
                const password = document.getElementById('register-password').value;
                const confirmPassword = document.getElementById('register-confirm-password').value;
                const resumeFile = document.getElementById('register-resume').files[0];
                const subscribe = document.getElementById('register-subscribe').checked;
                const agreeTerms = document.getElementById('register-terms').checked;
                
                if (password !== confirmPassword) {
                    showToast('Passwords do not match', 'error');
                    return;
                }
                
                if (!resumeFile) {
                    showToast('Please upload a resume', 'error');
                    return;
                }
                
                if (!agreeTerms) {
                    showToast('Please agree to the terms and conditions', 'error');
                    return;
                }
                
                // Create user
                auth.createUserWithEmailAndPassword(email, password)
                    .then((userCredential) => {
                        const user = userCredential.user;
                        
                        // Upload resume
                        const resumeRef = storage.ref(`resumes/${user.uid}/${resumeFile.name}`);
                        return resumeRef.put(resumeFile)
                            .then(() => resumeRef.getDownloadURL())
                            .then((url) => {
                                // Save user data
                                return db.collection('users').doc(user.uid).set({
                                    name: name,
                                    email: email,
                                    resume: url,
                                    resumeName: resumeFile.name,
                                    subscribe: subscribe,
                                    createdAt: new Date()
                                });
                            })
                            .then(() => {
                                // Update user profile
                                return user.updateProfile({
                                    displayName: name
                                });
                            });
                    })
                    .then(() => {
                        userRegisterModal.classList.remove('active');
                        showToast('Registration successful!', 'success');
                    })
                    .catch((error) => {
                        showToast('Registration error: ' + error.message, 'error');
                    });
            });
            
            // Set up forgot password form
            document.getElementById('forgot-submit-btn').addEventListener('click', () => {
                const email = document.getElementById('forgot-email').value;
                
                auth.sendPasswordResetEmail(email)
                    .then(() => {
                        showToast('Password reset email sent!', 'success');
                        forgotPasswordModal.classList.remove('active');
                    })
                    .catch((error) => {
                        showToast('Error: ' + error.message, 'error');
                    });
            });
            
            // Set up application form
            document.getElementById('application-submit-btn').addEventListener('click', () => {
                const name = document.getElementById('applicant-name').value;
                const email = document.getElementById('applicant-email').value;
                const phone = document.getElementById('applicant-phone').value;
                const resumeFile = document.getElementById('application-resume').files[0];
                const coverLetter = document.getElementById('application-cover-letter').value;
                
                // Get the job being applied for from the modal title
                const jobTitle = document.getElementById('apply-job-title').textContent;
                const companyName = document.getElementById('apply-company-name').textContent;
                
                // In a real application, you would save this to Firestore
                // and handle file uploads
                
                showToast('Application submitted successfully!', 'success');
                applicationModal.classList.remove('active');
            });
            
            // Handle file input changes
            document.querySelectorAll('.file-input').forEach(input => {
                input.addEventListener('change', (e) => {
                    const fileName = e.target.files[0]?.name || 'No file chosen';
                    const fileNameElement = e.target.parentElement.querySelector('.file-name');
                    if (fileNameElement) {
                        fileNameElement.textContent = fileName;
                    }
                });
            });
        }

        // Load user dashboard data
        function loadUserDashboard() {
            if (!currentUser) return;
            
            // Load user data
            db.collection('users').doc(currentUser.uid).get()
                .then((doc) => {
                    if (doc.exists) {
                        const userData = doc.data();
                        document.getElementById('dashboard-user-name').textContent = userData.name;
                        document.getElementById('dashboard-user-email').textContent = userData.email;
                        document.getElementById('dashboard-user-phone').textContent = userData.phone || 'Not provided';
                        document.getElementById('dashboard-user-age').textContent = userData.age || 'Not provided';
                        document.getElementById('primary-resume-name').textContent = userData.resumeName || 'No resume';
                    }
                });
            
            // Load saved jobs (placeholder)
            document.getElementById('saved-jobs-list').innerHTML = '<p>No saved jobs yet.</p>';
            
            // Load applied jobs (placeholder)
            document.getElementById('applied-jobs-list').innerHTML = '<p>You haven\'t applied to any jobs yet.</p>';
        }

        // Start the application
        init();
    </script>
</body>
</html>
