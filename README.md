# theme.liquid
<!doctype html>
<html class="no-js" lang="{{ request.locale.iso_code }}" dir="{{ settings.text_direction }}">
<head>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <meta name="theme-color" content="{{ settings.color_button }}">
  <link rel="canonical" href="{{ canonical_url }}">
  <link rel="preconnect" href="https://cdn.shopify.com" crossorigin>
  <link rel="preconnect" href="https://fonts.shopifycdn.com" crossorigin>
  <link rel="dns-prefetch" href="https://productreviews.shopifycdn.com">
  <link rel="dns-prefetch" href="https://ajax.googleapis.com">
  <link rel="dns-prefetch" href="https://maps.googleapis.com">
  <link rel="dns-prefetch" href="https://maps.gstatic.com">

  {%- if settings.favicon != blank -%}
    <link rel="shortcut icon" href="{{ settings.favicon | img_url: '32x32' }}" type="image/png" />
  {%- endif -%}

  {%- render 'seo-title' -%}

  {%- if page_description -%}
  <meta name="description" content="{{ page_description | escape }}">
  {%- endif -%}

  {%- render 'social-meta-tags' -%}

  {{ content_for_header }}

  <script>
    var theme = {
      stylesheet: "{{ 'theme.css' | asset_url }}",
      template: {{ template | json }},
      routes: {
        home: "{{ routes.root_url }}",
        cart: "{{ routes.cart_url | append: '.js' }}",
        cartPage: "{{ routes.cart_url }}",
        cartAdd: "{{ routes.cart_add_url | append: '.js'}}",
        cartChange: "{{ routes.cart_change_url | append: '.js' }}",
        predictiveSearch: "{{ routes.predictive_search_url }}"
      },
      strings: {
        addToCart: {{ 'products.product.add_to_cart' | t | json }},
        soldOut: {{ 'products.product.sold_out' | t | json }},
        unavailable: {{ 'products.product.unavailable' | t | json }},
        regularPrice: {{ 'products.general.regular_price' | t | json }},
        salePrice: {{ 'products.general.sale_price' | t | json }},
        inStockLabel: {{ 'products.product.in_stock_label' | t | json }},
        oneStockLabel: {{ 'products.product.stock_label.one' | t: count: '[count]' | json }},
        otherStockLabel: {{ 'products.product.stock_label.other' | t: count: '[count]' | json }},
        willNotShipUntil: {{ 'products.product.will_not_ship_until' | t: date: '[date]' | json }},
        willBeInStockAfter: {{ 'products.product.will_be_in_stock_after' | t: date: '[date]' | json }},
        waitingForStock: {{ 'products.product.waiting_for_stock' | t | json }},
        cartItems: {{ 'cart.general.item_count' | t: count: '[count]' | json }},
        cartConfirmDelete: {{ 'cart.general.delete_confirm' | t | json }},
        cartTermsConfirmation: {{ 'cart.general.terms_confirm' | t | json }},
        maxQuantity: {{ 'cart.general.max_quantity' | t: quantity: '[quantity]', title: '[title]' | json }}
      },
      settings: {
        cartType: {{ settings.cart_type | json }},
        isCustomerTemplate: {% if request.page_type contains 'customers/' %}true{% else %}false{% endif %},
        moneyFormat: {{ shop.money_format | json }},
        quickView: {{ settings.quick_shop_enable }},
        hoverProductGrid: {{ settings.product_hover_image }},
        themeName: 'Streamline',
        themeVersion: "7.0.0",
        predictiveSearchType: {{ settings.search_type | json }},
      }
    };

    document.documentElement.className = document.documentElement.className.replace('no-js', 'js');
  </script>

  {%- render 'css-variables' -%}
  {%- render 'critical-css' -%}
  {{ 'theme.css' | asset_url | stylesheet_tag: preload: true }}

  {%- if shop.enabled_currencies.size > 1 -%}
    <link rel="stylesheet" href="{{ 'country-flags.css' | asset_url | split: '?' | first }}">
  {%- endif -%}

  <style>
  /*
    🔥 HARLEY VAPE - DESIGN SYSTEM COMPLET
    =====================================
    Header existant + Palette optimisée Claude x Luma + Composants TRUFF-style
  */

  /* ========================================
     🎨 PALETTE HARLEY VAPE - VARIABLES GLOBALES
     ======================================== */

  :root {
    /* === COULEURS PRINCIPALES === */
    --hv-orange-punchy: #FF7A2D;
    --hv-abricot-doux: #F7C38B;
    --hv-caramel-soleil: #E88C4D;
    --hv-miel-retro: #F3B97F;
    --hv-vanille-solaire: #FFEBD3;
    --hv-rouge-bandana: #D62A2A;
    --hv-violet-harley: #8B4DFF;
    --hv-bleu-vintage: #1F3F6F;
    --hv-marron-doux: #8B4513;
    
    /* === COULEURS DÉRIVÉES === */
    --hv-orange-light: rgba(255, 122, 45, 0.1);
    --hv-orange-medium: rgba(255, 122, 45, 0.3);
    --hv-orange-strong: rgba(255, 122, 45, 0.7);
    --hv-white-warm: #FFF8F2;
    --hv-gray-warm: #F5F0EA;
    
    /* === GRADIENTS SIGNATURE === */
    --hv-gradient-sunset: linear-gradient(135deg, var(--hv-orange-punchy), var(--hv-caramel-soleil));
    --hv-gradient-warm: linear-gradient(90deg, var(--hv-vanille-solaire), var(--hv-abricot-doux));
    --hv-gradient-hero: linear-gradient(45deg, var(--hv-miel-retro), var(--hv-orange-punchy), var(--hv-rouge-bandana));
    --hv-gradient-header: linear-gradient(180deg, #f2e6d0 0%, #ebd5b8 25%, #e4c49a 50%, #ddb37c 75%, #d6a25e 100%);
    
    /* === OMBRES SIGNATURE === */
    --hv-shadow-soft: 0 4px 12px rgba(255, 122, 45, 0.15);
    --hv-shadow-medium: 0 8px 24px rgba(232, 140, 77, 0.25);
    --hv-shadow-strong: 0 12px 36px rgba(255, 122, 45, 0.4);
    --hv-shadow-drop: 0 6px 16px rgba(214, 42, 42, 0.5);
    
    /* === ANIMATIONS === */
    --hv-transition-fast: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
    --hv-transition-smooth: all 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
    --hv-transition-bounce: all 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55);
    
    /* === TYPOGRAPHIE === */
    --hv-font-weight-light: 300;
    --hv-font-weight-normal: 400;
    --hv-font-weight-bold: 700;
    --hv-font-weight-black: 900;
    
    /* === ESPACEMENTS === */
    --hv-space-xs: 4px;
    --hv-space-sm: 8px;
    --hv-space-md: 16px;
    --hv-space-lg: 24px;
    --hv-space-xl: 32px;
    --hv-space-xxl: 48px;
    
    /* === BORDER RADIUS === */
    --hv-radius-sm: 6px;
    --hv-radius-md: 12px;
    --hv-radius-lg: 20px;
    --hv-radius-full: 50px;
  }

  /* ========================================
     🌊 TEXTE DÉFILANT ORANGE - VITESSE OPTIMISÉE
     ======================================== */

  /* Cibler TOUTES les sections de texte défilant */
  .scrolling-text-section,
  .marquee-section,
  [data-section-type="scrolling-text"],
  .shopify-section[id*="scrolling"],
  .shopify-section[id*="text"],
  .shopify-section[id*="marquee"],
  section[id*="scrolling_text"],
  section[id*="AYWMeG"],
  .section-scrolling-text,
  .section-marquee,
  #shopify-section-scrolling_text_AYWMeG,
  [id*="scrolling_text_AYWMeG"] {
    background: var(--hv-gradient-sunset) !important;
    color: var(--hv-vanille-solaire) !important;
    font-family: 'Georgia', serif !important;
    font-size: 14px !important;
    font-weight: 500 !important;
    text-align: center !important;
    padding: 8px 0 !important;
    position: relative !important;
    z-index: 1001 !important;
    white-space: nowrap !important;
    overflow: hidden !important;
    display: block !important;
    visibility: visible !important;
    opacity: 1 !important;
    height: auto !important;
    min-height: 35px !important;
    max-height: none !important;
    width: 100% !important;
    left: 0 !important;
    right: 0 !important;
    margin: 0 !important;
    order: -2 !important;
  }

  /* Texte qui défile - VITESSE OPTIMISÉE */
  .scrolling-text,
  .marquee__content,
  .scrolling-text-section .marquee__content,
  .marquee-text,
  .marquee__text,
  [class*="scrolling"] [class*="content"],
  [class*="marquee"] [class*="content"],
  #shopify-section-scrolling_text_AYWMeG .marquee,
  #shopify-section-scrolling_text_AYWMeG .marquee__content,
  #shopify-section-scrolling_text_AYWMeG .scrolling-text,
  [id*="scrolling_text_AYWMeG"] .marquee,
  [id*="scrolling_text_AYWMeG"] .marquee__content,
  [id*="scrolling_text_AYWMeG"] [class*="marquee"],
  [id*="scrolling_text_AYWMeG"] [class*="content"] {
    display: inline-block !important;
    animation: scroll-horizontal-perfect 120s linear infinite !important;
    white-space: nowrap !important;
    color: inherit !important;
    visibility: visible !important;
    opacity: 1 !important;
    font-size: inherit !important;
    font-family: inherit !important;
  }

  @keyframes scroll-horizontal-perfect {
    0% { transform: translateX(100%); }
    100% { transform: translateX(-100%); }
  }

  /* ========================================
     📢 BARRE D'ANNONCE ORANGE - PARFAITE
     ======================================== */

  .announcement,
  .announcement-bar,
  [data-section-type="announcement-bar"],
  .shopify-section[id*="announcement"],
  section[id*="announcement"],
  .section-announcement,
  .section-announcement-bar,
  .announcement-section,
  .announcement-bar-section {
    background: var(--hv-gradient-warm) !important;
    color: var(--hv-marron-doux) !important;
    font-family: 'Georgia', serif !important;
    font-size: 13px !important;
    font-weight: 600 !important;
    text-align: center !important;
    padding: 10px 0 !important;
    position: relative !important;
    z-index: 1000 !important;
    display: block !important;
    visibility: visible !important;
    opacity: 1 !important;
    height: auto !important;
    min-height: 35px !important;
    order: -1 !important;
  }

  .announcement__text,
  .announcement__link,
  .announcement-bar__text,
  .announcement-bar__link,
  .announcement__message,
  .announcement-bar__message {
    color: inherit !important;
    text-decoration: none !important;
    font-weight: inherit !important;
  }

  .announcement__link:hover,
  .announcement-bar__link:hover {
    opacity: 0.9 !important;
    color: var(--hv-rouge-bandana) !important;
  }

  /* ========================================
     🎨 HEADER PRINCIPAL - COULEURS HARLEY OPTIMISÉES
     ======================================== */

  .site-header {
    background: var(--hv-gradient-header) !important;
    position: relative !important;
    z-index: 999 !important;
    padding: 25px 0 30px !important;
    
    /* RELIEF ULTRA-AUTHENTIQUE */
    box-shadow: 
      0 6px 20px rgba(0, 0, 0, 0.25),
      0 12px 40px rgba(139, 69, 19, 0.18),
      0 20px 60px rgba(160, 82, 45, 0.12),
      inset 0 3px 0 rgba(255, 248, 235, 0.8),
      inset 0 -3px 0 rgba(139, 69, 19, 0.25),
      inset 6px 0 12px rgba(240, 213, 184, 0.4),
      inset -6px 0 12px rgba(240, 213, 184, 0.4) !important;
    
    border-top: 4px solid var(--hv-vanille-solaire) !important;
    border-bottom: 5px solid var(--hv-marron-doux) !important;
    border-left: none !important;
    border-right: none !important;
    
    transition: var(--hv-transition-smooth) !important;
    order: 0 !important;
  }

  /* Bandes décoratives VISIBLES */
  .site-header::before {
    content: '' !important;
    position: absolute !important;
    top: 0 !important;
    left: 0 !important;
    right: 0 !important;
    height: 3px !important;
    background: linear-gradient(90deg, 
      transparent,
      rgba(255, 248, 235, 0.9) 20%,
      rgba(255, 255, 255, 1) 50%,
      rgba(255, 248, 235, 0.9) 80%,
      transparent
    ) !important;
    z-index: 10 !important;
  }

  .site-header::after {
    content: '' !important;
    position: absolute !important;
    bottom: 0 !important;
    left: 15px !important;
    right: 15px !important;
    height: 2px !important;
    background: linear-gradient(90deg, 
      rgba(139, 69, 19, 0.3),
      rgba(139, 69, 19, 0.8) 50%,
      rgba(139, 69, 19, 0.3)
    ) !important;
    z-index: 10 !important;
  }

  /* ========================================
     🎯 LOGO AVEC EFFETS FUMÉE RENFORCÉS
     ======================================== */

  .header-item--logo {
    position: relative !important;
    display: flex !important;
    align-items: center !important;
    justify-content: center !important;
    z-index: 120 !important;
    overflow: visible !important;
    flex: 0 0 auto !important;
  }

  /* 💨 EFFET FUMÉE GAUCHE - RENFORCÉ */
  .header-item--logo::before {
    content: '' !important;
    position: absolute !important;
    top: -12px !important;
    left: -20px !important;
    width: 35px !important;
    height: 30px !important;
    background: radial-gradient(circle, 
      rgba(255, 255, 255, 0.8) 0%,
      rgba(248, 244, 230, 0.6) 30%,
      rgba(240, 232, 208, 0.4) 60%,
      rgba(232, 218, 184, 0.2) 80%,
      transparent 100%
    ) !important;
    border-radius: 50% 60% 40% 50% !important;
    filter: blur(1.5px) !important;
    opacity: 0.8 !important;
    z-index: -1 !important;
    animation: float-left-enhanced 6s ease-in-out infinite !important;
  }

  /* 💨 EFFET FUMÉE DROITE - RENFORCÉ */
  .header-item--logo::after {
    content: '' !important;
    position: absolute !important;
    top: -15px !important;
    right: -25px !important;
    width: 40px !important;
    height: 25px !important;
    background: radial-gradient(ellipse, 
      rgba(255, 255, 255, 0.7) 0%,
      rgba(248, 244, 230, 0.5) 40%,
      rgba(232, 218, 184, 0.3) 70%,
      rgba(214, 192, 154, 0.1) 90%,
      transparent 100%
    ) !important;
    border-radius: 60% 40% 50% 60% !important;
    filter: blur(1.2px) !important;
    opacity: 0.7 !important;
    z-index: -1 !important;
    animation: float-right-enhanced 7s ease-in-out infinite reverse !important;
  }

  /* 🌊 ANIMATIONS FLOTTANTES AMÉLIORÉES */
  @keyframes float-left-enhanced {
    0%, 100% { 
      transform: translateY(0px) scale(1) rotate(0deg);
      opacity: 0.8;
    }
    25% { 
      transform: translateY(-4px) scale(1.08) rotate(2deg);
      opacity: 0.9;
    }
    50% { 
      transform: translateY(-3px) scale(0.92) rotate(-1deg);
      opacity: 0.7;
    }
    75% { 
      transform: translateY(-6px) scale(1.05) rotate(1deg);
      opacity: 0.85;
    }
  }

  @keyframes float-right-enhanced {
    0%, 100% { 
      transform: translateY(0px) translateX(0px) scale(1) rotate(0deg);
      opacity: 0.7;
    }
    30% { 
      transform: translateY(-3px) translateX(3px) scale(1.12) rotate(-2deg);
      opacity: 0.8;
    }
    60% { 
      transform: translateY(-7px) translateX(-2px) scale(0.88) rotate(1deg);
      opacity: 0.6;
    }
    80% { 
      transform: translateY(-4px) translateX(2px) scale(1.06) rotate(-1deg);
      opacity: 0.75;
    }
  }

  /* Hover effects intensifiés */
  .header-item--logo:hover::before {
    width: 45px !important;
    height: 35px !important;
    opacity: 1 !important;
    filter: blur(1px) !important;
    animation-duration: 3s !important;
  }

  .header-item--logo:hover::after {
    width: 50px !important;
    height: 30px !important;
    opacity: 0.9 !important;
    filter: blur(0.8px) !important;
    animation-duration: 4s !important;
  }

  /* LOGO RELIEF ULTRA-RENFORCÉ */
  .header-item--logo img {
    height: auto !important;
    max-height: 70px !important; 
    width: auto !important;
    transform: scale(1.8) !important; 
    transform-origin: center !important;
    
    filter: 
      drop-shadow(4px 4px 0 var(--hv-orange-punchy)) 
      drop-shadow(-3px -3px 0 var(--hv-rouge-bandana))
      drop-shadow(0 8px 16px rgba(0, 0, 0, 0.4))
      drop-shadow(0 16px 32px rgba(139, 69, 19, 0.3))
      drop-shadow(2px 2px 4px var(--hv-caramel-soleil))
      contrast(1.2)
      saturate(1.3)
      brightness(1.1) !important;
    
    position: relative !important;
    z-index: 15 !important;
    transition: var(--hv-transition-bounce) !important;
  }

  .header-item--logo:hover img {
    transform: scale(1.9) rotate(2deg) !important;
    filter: 
      drop-shadow(5px 5px 0 var(--hv-orange-punchy)) 
      drop-shadow(-4px -4px 0 var(--hv-rouge-bandana))
      drop-shadow(0 10px 20px rgba(0, 0, 0, 0.45))
      drop-shadow(0 20px 40px rgba(139, 69, 19, 0.35))
      drop-shadow(3px 3px 6px var(--hv-caramel-soleil))
      contrast(1.25)
      saturate(1.35)
      brightness(1.15) !important;
  }

  /* ========================================
     🔥 BADGE DROP ULTRA-VISIBLE
     ======================================== */

  .badge-promo {
    position: absolute !important;
    top: -15px !important;
    right: -30px !important;
    
    background: var(--hv-gradient-hero) !important;
    color: white !important;
    font-size: 11px !important;
    font-weight: var(--hv-font-weight-black) !important;
    padding: 5px 10px 4px !important;
    border-radius: var(--hv-radius-md) !important;
    text-transform: uppercase !important;
    letter-spacing: 0.6px !important;
    
    box-shadow: var(--hv-shadow-drop) !important;
    transform: rotate(-8deg) !important;
    z-index: 30 !important;
    transition: var(--hv-transition-bounce) !important;
    animation: hvPulse 2s infinite !important;
  }

  @keyframes hvPulse {
    0%, 100% { transform: rotate(-8deg) scale(1); }
    50% { transform: rotate(-8deg) scale(1.05); }
  }

  .badge-promo:hover {
    transform: rotate(-5deg) scale(1.1) !important;
    box-shadow: var(--hv-shadow-strong) !important;
  }

  /* ========================================
     🔗 NAVIGATION STYLÉE PARFAITE
     ======================================== */

  .site-header .site-nav {
    display: flex !important;
    align-items: center !important;
    gap: var(--hv-space-xl) !important;
    justify-content: center !important;
  }

  .site-header .site-nav__link {
    position: relative !important;
    color: var(--hv-marron-doux) !important;
    font-weight: var(--hv-font-weight-bold) !important;
    font-size: 16px !important;
    text-decoration: none !important;
    padding: var(--hv-space-sm) var(--hv-space-md) !important;
    border-radius: var(--hv-radius-sm) !important;
    transition: var(--hv-transition-smooth) !important;
    text-transform: uppercase !important;
    letter-spacing: 0.5px !important;
    font-family: 'Helvetica Neue', Arial, sans-serif !important;
  }

  .site-header .site-nav__link:hover {
    color: var(--hv-orange-punchy) !important;
    background: var(--hv-orange-light) !important;
    transform: translateY(-1px) !important;
    box-shadow: var(--hv-shadow-soft) !important;
  }

  /* ========================================
     🔘 ICÔNES DROITE PARFAITES
     ======================================== */

  .header-item--icons {
    display: flex !important;
    align-items: center !important;
    gap: var(--hv-space-lg) !important;
    margin-left: auto !important;
  }

  .header-item--icons a {
    position: relative !important;
    display: inline-flex !important;
    align-items: center !important;
    justify-content: center !important;
    padding: 10px !important;
    border-radius: 10px !important;
    transition: var(--hv-transition-smooth) !important;
    background: rgba(255, 255, 255, 0.6) !important;
    box-shadow: var(--hv-shadow-soft) !important;
  }

  .header-item--icons a:hover {
    transform: translateY(-2px) !important;
    box-shadow: var(--hv-shadow-medium) !important;
    background: var(--hv-orange-light) !important;
  }

  .header-item--icons svg {
    width: 20px !important;
    height: 20px !important;
    color: var(--hv-marron-doux) !important;
    transition: var(--hv-transition-fast) !important;
  }

  .header-item--icons a:hover svg {
    color: var(--hv-orange-punchy) !important;
    transform: scale(1.1) !important;
  }

  /* Badge panier */
  .cart-link__bubble {
    position: absolute !important;
    top: -6px !important;
    right: -6px !important;
    background: var(--hv-gradient-sunset) !important;
    color: white !important;
    font-size: 11px !important;
    font-weight: var(--hv-font-weight-bold) !important;
    padding: 2px 6px !important;
    border-radius: var(--hv-radius-sm) !important;
    box-shadow: var(--hv-shadow-drop) !important;
    transform: scale(0.9) !important;
    transition: var(--hv-transition-fast) !important;
  }

  .cart-link__bubble--visible {
    transform: scale(1) !important;
  }

  /* ========================================
     🎨 NOUVELLES CLASSES UTILITAIRES HARLEY VAPE
     ======================================== */

  /* === BACKGROUNDS === */
  .hv-bg-orange { background: var(--hv-orange-punchy) !important; }
  .hv-bg-vanille { background: var(--hv-vanille-solaire) !important; }
  .hv-bg-caramel { background: var(--hv-caramel-soleil) !important; }
  .hv-bg-gradient-sunset { background: var(--hv-gradient-sunset) !important; }
  .hv-bg-gradient-warm { background: var(--hv-gradient-warm) !important; }
  .hv-bg-warm { background: var(--hv-white-warm) !important; }

  /* === TEXTES === */
  .hv-text-orange { color: var(--hv-orange-punchy) !important; }
  .hv-text-caramel { color: var(--hv-caramel-soleil) !important; }
  .hv-text-bandana { color: var(--hv-rouge-bandana) !important; }
  .hv-text-violet { color: var(--hv-violet-harley) !important; }
  .hv-text-vintage { color: var(--hv-bleu-vintage) !important; }
  .hv-text-marron { color: var(--hv-marron-doux) !important; }

  /* === BOUTONS SIGNATURE === */
  .hv-btn-primary {
    background: var(--hv-gradient-sunset);
    color: white;
    border: none;
    border-radius: var(--hv-radius-md);
    padding: 14px 28px;
    font-weight: var(--hv-font-weight-bold);
    font-size: 16px;
    letter-spacing: 0.5px;
    text-transform: uppercase;
    cursor: pointer;
    transition: var(--hv-transition-smooth);
    box-shadow: var(--hv-shadow-medium);
    position: relative;
    overflow: hidden;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    text-decoration: none;
    min-height: 48px;
  }

  .hv-btn-primary::before {
    content: '';
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
    transition: var(--hv-transition-smooth);
  }

  .hv-btn-primary:hover {
    transform: translateY(-2px) scale(1.02);
    box-shadow: var(--hv-shadow-strong);
    color: white;
    text-decoration: none;
  }

  .hv-btn-primary:hover::before {
    left: 100%;
  }

  .hv-btn-secondary {
    background: transparent;
    color: var(--hv-orange-punchy);
    border: 2px solid var(--hv-orange-punchy);
    border-radius: var(--hv-radius-md);
    padding: 12px 24px;
    font-weight: var(--hv-font-weight-bold);
    transition: var(--hv-transition-smooth);
    cursor: pointer;
    text-decoration: none;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    min-height: 48px;
  }

  .hv-btn-secondary:hover {
    background: var(--hv-orange-punchy);
    color: white;
    transform: translateY(-1px);
    box-shadow: var(--hv-shadow-medium);
    text-decoration: none;
  }

  /* === CARDS PRODUITS TRUFF-STYLE === */
  .hv-product-card {
    background: white;
    border-radius: var(--hv-radius-md);
    padding: var(--hv-space-lg);
    box-shadow: var(--hv-shadow-soft);
    transition: var(--hv-transition-smooth);
    border: 1px solid var(--hv-gray-warm);
    overflow: hidden;
    position: relative;
    display: block;
    text-decoration: none;
    color: inherit;
  }

  .hv-product-card:hover {
    transform: translateY(-8px);
    box-shadow: var(--hv-shadow-strong);
    border-color: var(--hv-orange-punchy);
    text-decoration: none;
    color: inherit;
  }

  .hv-product-card::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 4px;
    background: var(--hv-gradient-sunset);
    transform: scaleX(0);
    transition: var(--hv-transition-smooth);
  }

  .hv-product-card:hover::after {
    transform: scaleX(1);
  }

  .hv-product-card__image {
    width: 100%;
    height: 200px;
    object-fit: cover;
    border-radius: var(--hv-radius-sm);
    margin-bottom: var(--hv-space-md);
  }

  .hv-product-card__title {
    font-size: 18px;
    font-weight: var(--hv-font-weight-bold);
    color: var(--hv-marron-doux);
    margin-bottom: var(--hv-space-sm);
    line-height: 1.3;
  }

  .hv-product-card__price {
    font-size: 16px;
    font-weight: var(--hv-font-weight-bold);
    color: var(--hv-orange-punchy);
    margin-bottom: var(--hv-space-md);
  }

  /* === GRILLE PRODUITS TRUFF-STYLE === */
  .hv-products-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: var(--hv-space-xl);
    padding: var(--hv-space-xl);
  }

  /* === NAVIGATION LATÉRALE TRUFF-STYLE === */
  .hv-sidebar-nav {
    background: var(--hv-white-warm);
    padding: var(--hv-space-xl);
    border-radius: var(--hv-radius-md);
    box-shadow: var(--hv-shadow-soft);
  }

  .hv-sidebar-nav__title {
    font-size: 20px;
    font-weight: var(--hv-font-weight-bold);
    color: var(--hv-marron-doux);
    margin-bottom: var(--hv-space-lg);
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }

  .hv-sidebar-nav__list {
    list-style: none;
    padding: 0;
    margin: 0;
  }

  .hv-sidebar-nav__item {
    margin-bottom: var(--hv-space-sm);
  }

  .hv-sidebar-nav__link {
    display: block;
    padding: var(--hv-space-sm) var(--hv-space-md);
    color: var(--hv-marron-doux);
    text-decoration: none;
    border-radius: var(--hv-radius-sm);
    transition: var(--hv-transition-fast);
    font-weight: var(--hv-font-weight-normal);
  }

  .hv-sidebar-nav__link:hover,
  .hv-sidebar-nav__link--active {
    background: var(--hv-orange-light);
    color: var(--hv-orange-punchy);
    transform: translateX(4px);
  }

  /* === UTILITAIRES OMBRES === */
  .hv-shadow-soft { box-shadow: var(--hv-shadow-soft) !important; }
  .hv-shadow-medium { box-shadow: var(--hv-shadow-medium) !important; }
  .hv-shadow-strong { box-shadow: var(--hv-shadow-strong) !important; }

  /* === UTILITAIRES BORDURES === */
  .hv-border-orange { border-color: var(--hv-orange-punchy) !important; }
  .hv-border-caramel { border-color: var(--hv-caramel-soleil) !important; }

  /* === ANIMATIONS CUSTOM === */
  @keyframes hvSlideIn {
    from {
      opacity: 0;
      transform: translateY(30px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  .hv-animate-slide-in {
    animation: hvSlideIn 0.6s var(--hv-transition-smooth);
  }

  /* ========================================
     📱 MOBILE OPTIMISÉ
     ======================================== */

  @media (max-width: 768px) {
    .site-header {
      padding: 20px 0 25px !important;
    }
    
    .header-item--logo img {
      max-height: 55px !important;
      transform: scale(1.5) !important;
    }
    
    .badge-promo {
      font-size: 9px !important;
      padding: 3px 7px !important;
      top: -10px !important;
      right: -25px !important;
    }
    
    .site-header .site-nav {
      gap: 18px !important;
    }
    
    .site-header .site-nav__link {
      font-size: 14px !important;
      padding: 6px 12px !important;
    }
    
    /* Texte défilant mobile */
    #shopify-section-scrolling_text_AYWMeG,
    [id*="scrolling_text_AYWMeG"] {
      font-size: 12px !important;
      padding: 6px 0 !important;
    }

    .hv-products-grid {
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: var(--hv-space-lg);
      padding: var(--hv-space-lg);
    }

    .hv-btn-primary,
    .hv-btn-secondary {
      width: 100%;
      justify-content: center;
    }
  }

  @media (max-width: 480px) {
    .header-item--logo img {
      max-height: 50px !important;
      transform: scale(1.4) !important;
    }
    
    .badge-promo {
      font-size: 8px !important;
      padding: 2px 6px !important;
      top: -8px !important;
      right: -20px !important;
    }
    
    .site-header .site-nav__link {
      font-size: 12px !important;
      padding: 4px 8px !important;
    }
    
    /* Texte défilant très petit écran */
    #shopify-section-scrolling_text_AYWMeG,
    [id*="scrolling_text_AYWMeG"] {
      font-size: 11px !important;
      padding: 5px 0 !important;
    }

    .hv-products-grid {
      grid-template-columns: 1fr;
      padding: var(--hv-space-md);
    }
  }

  /* ========================================
     🛡️ FORÇAGE GLOBAL D'AFFICHAGE
     ======================================== */

  .shopify-section {
    display: block !important;
    visibility: visible !important;
    opacity: 1 !important;
  }

  .header-wrapper .shopify-section,
  [data-section-group="header-group"] .shopify-section,
  .header-group .shopify-section {
    display: block !important;
    visibility: visible !important;
    opacity: 1 !important;
    position: relative !important;
  }

  .header-wrapper {
    position: relative !important;
    z-index: 100 !important;
  }

  #shopify-section-scrolling_text_AYWMeG,
  #shopify-section-announcement-bar,
  #shopify-section-header {
    display: block !important;
    visibility: visible !important;
    opacity: 1 !important;
  }

  .header-wrapper > .shopify-section:first-child,
  [data-section-group="header-group"] > .shopify-section:first-child {
    display: block !important;
    visibility: visible !important;
    opacity: 1 !important;
  }

  .main-content {
    padding-top: 20px !important;
    position: relative !important;
    z-index: 10 !important;
  }

  /* === SPÉCIAL SHOPIFY === */
  .shopify-section .hv-btn-primary {
    min-height: 44px;
  }

  .product-form .hv-btn-primary {
    width: 100%;
    margin-top: var(--hv-space-md);
  }

  /* === OPTIMISATIONS PERFORMANCE === */
  * {
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  .hv-product-card,
  .hv-btn-primary,
  .site-nav__link {
    will-change: transform;
  }
  </style>

  <script src="{{ 'vendor-v6.js' | asset_url | split: '?' | first }}" defer="defer"></script>
  <script src="{{ 'theme.js' | asset_url }}" defer="defer"></script>

  {%- if request.page_type contains 'customers/' -%}
    <script src="{{ 'shopify_common.js' | shopify_asset_url }}" defer="defer"></script>
  {%- endif -%}

  {% if request.design_mode %}
    <script>theme.settings.email = {{ shop.email | json }}</script>
    <script src="https://api.archetypethemes.co/design-mode.js" defer="defer"></script>
  {% endif %}
</head>

<body class="template-{{ template | replace: '.', ' ' | truncatewords: 1, '' | handle }}{% if request.path == '/challenge' %} template-challange{% endif %}{% if settings.cart_type == 'sticky' and cart.item_count > 0 and template != 'cart' %} body--sticky-cart-open{% endif %}{% if cart.item_count > 0 %} cart-has-items{% endif %}" ontouchstart="return true;" data-transitions="{{settings.animate_page_transitions}}" data-animate_underlines="true" data-animate_images="{{settings.animate_images}}" data-button_style="{{settings.button_style}}" data-type_product_capitalize="{{settings.type_product_capitalize}}" data-type_header_capitalize="{{settings.type_header_capitalize}}" data-product_image_scatter="{{settings.product_image_scatter}}" data-button_type_style="{{settings.button_type_style}}">
  <div id="OverscrollLoader" class="overscroll-loader" aria-hidden="true">
    <svg aria-hidden="true" focusable="false" role="presentation" class="icon icon--full-color icon-loader--full-color"><path class="icon-loader__close" d="m19 17.61 27.12 27.13m0-27.12L19 44.74"/><path class="icon-loader__path" d="M40 90a40 40 0 1 1 20 0"/></svg>
  </div>

  <div class="root">

    {%- if settings.animate_page_transitions -%}
      <script>window.setTimeout(function() { document.body.className += " loaded"; }, 25);</script>
    {%- endif -%}

    <div class="splash-screen">
      {%- if settings.animate_page_transitions and settings.logo_loader_image != blank -%}
        <div class="splash-screen__loader">
          {% comment %} Desktop logo {% endcomment %}
          {%- assign width = settings.logo_loader_image.width | times: 2 -%}
          {%- assign height = settings.logo_loader_image.width | divided_by: settings.logo_loader_image.aspect_ratio -%}
          {%- capture sizes -%}{{ settings.desktop_loader_width }}px{%- endcapture -%}
          {%- capture widths -%}{{ settings.desktop_loader_width }}, {{ settings.desktop_loader_width | times: 2 }}{%- endcapture -%}
          {%- capture style -%}max-height: {{ settings.desktop_loader_width | divided_by: settings.logo_loader_image.aspect_ratio }}px;max-width: {{ settings.desktop_loader_width }}px;{%- endcapture -%}

          {% comment %} Mobile logo {% endcomment %}
          {%- assign mobile_height = settings.mobile_loader_width | times: 2 -%}
          {%- assign mobile_height = settings.mobile_loader_width | divided_by: settings.logo_loader_image.aspect_ratio -%}
          {%- capture mobile_sizes -%}{{ settings.mobile_loader_width }}px{%- endcapture -%}
          {%- capture mobile_widths -%}{{ settings.mobile_loader_width }}, {{ settings.mobile_loader_width | times: 2 }}{%- endcapture -%}
          {%- capture mobile_style -%}max-height: {{ settings.mobile_loader_width | divided_by: settings.logo_loader_image.aspect_ratio }}px;max-width: {{ settings.mobile_loader_width }}px;{%- endcapture -%}

          {%- render 'image-element',
            img: settings.logo_loader_image,
            classes: 'loader-logo__img small--hide',
            img_width: width,
            img_height: height,
            sizes: sizes,
            widths: widths,
            style: style,
            ariaHidden: true,
          -%}

          {%- render 'image-element',
            img: settings.logo_loader_image,
            classes: 'loader-logo__img medium-up--hide',
            img_width: mobile_width,
            img_height: mobile_height
            sizes: mobile_sizes,
            widths: mobile_widths,
            style: mobile_style,
            ariaHidden: true,
          -%}
        </div>
      {%- else -%}
        <span class="loader-text">{{ 'general.accessibility.loading' | t }}</span>
      {%- endif -%}
    </div>

    <a class="in-page-link visually-hidden skip-link" href="#MainContent">{{ 'general.accessibility.skip_to_content' | t }}</a>

    <div id="PageContainer" class="page-container">
      <div class="transition-body">
        {%- sections 'header-group' -%}
        {%- sections 'popup-group' -%}

        <main class="main-content" id="MainContent">
          {{ content_for_layout }}
        </main>

        {%- sections 'footer-group' -%}
      </div>
    </div>

    {%- render 'video-modal' -%}
    {%- if settings.animate_page_transition_style == 'page-logo' -%}
      <div class="loader-logo">
        {%- if settings.logo_loader_image != blank -%}
          <div class="splash-screen__loader">
            {% comment %} Desktop logo {% endcomment %}
            {%- assign width = settings.logo_loader_image.width | times: 2 -%}
            {%- assign height = settings.logo_loader_image.width | divided_by: settings.logo_loader_image.aspect_ratio -%}
            {%- capture sizes -%}{{ settings.desktop_loader_width }}px{%- endcapture -%}
            {%- capture widths -%}{{ settings.desktop_loader_width }}, {{ settings.desktop_loader_width | times: 2 }}{%- endcapture -%}
            {%- capture style -%}max-height: {{ settings.desktop_loader_width | divided_by: settings.logo_loader_image.aspect_ratio }}px;max-width: {{ settings.desktop_loader_width }}px;{%- endcapture -%}

            {% comment %} Mobile logo {% endcomment %}
            {%- assign mobile_height = settings.mobile_loader_width | times: 2 -%}
            {%- assign mobile_height = settings.mobile_loader_width | divided_by: settings.logo_loader_image.aspect_ratio -%}
            {%- capture mobile_sizes -%}{{ settings.mobile_loader_width }}px{%- endcapture -%}
            {%- capture mobile_widths -%}{{ settings.mobile_loader_width }}, {{ settings.mobile_loader_width | times: 2 }}{%- endcapture -%}
            {%- capture mobile_style -%}max-height: {{ settings.mobile_loader_width | divided_by: settings.logo_loader_image.aspect_ratio }}px;max-width: {{ settings.mobile_loader_width }}px;{%- endcapture -%}

            {%- render 'image-element',
              img: settings.logo_loader_image,
              classes: 'loader-logo__img small--hide',
              img_width: width,
              img_height: height,
              sizes: sizes,
              widths: widths,
              style: style,
              ariaHidden: true,
            -%}

            {%- render 'image-element',
              img: settings.logo_loader_image,
              classes: 'loader-logo__img medium-up--hide',
              img_width: mobile_width,
              img_height: mobile_height
              sizes: mobile_sizes,
              widths: mobile_widths,
              style: mobile_style,
              ariaHidden: true,
            -%}
          </div>
        {%- else -%}
          <span class="loader-text">{{ 'general.accessibility.loading' | t }}</span>
        {%- endif -%}
      </div>
    {%- endif -%}
  </div>
  <div id="ProductScreens"></div>

  {%- liquid
    render 'photoswipe-template'
    if settings.cart_type == 'drawer'
      render 'cart-drawer'
    endif
    render 'tool-tip'
  -%}
</body>
</html>
