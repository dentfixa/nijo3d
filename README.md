# Nijo Castle 2 km — three.js (실사 3D ↔ 파스텔 화풍)

Real-time three.js scene of the area within 2 km of Nijo Castle (二条城), Kyoto.
Photoreal mode: PLATEAU LOD2 textured buildings, GSI aerial ground and real DEM mountains, leaf-card trees, procedural castle (ishigaki, plaster, gates, corner towers).
Modes: 궤도 (orbit) · 드론 (drone) · 걷기 (walk). Style toggle: button / S (orbit) / P (drone, walk).

Data & credits
- Map data © OpenStreetMap contributors, ODbL 1.0 (https://www.openstreetmap.org/copyright), extract via Geofabrik (kansai, 2026-11-13).
- Buildings: 3D都市モデル（Project PLATEAU）京都市（2025年度）, 国土交通省 — LOD2 textured 3D Tiles streamed from the PLATEAU CMS, used under the PLATEAU site policy (CC BY 4.0 compatible). https://www.mlit.go.jp/plateau/
- Ground photo and terrain: 国土地理院 地理院タイル (全国最新写真（シームレス）seamlessphoto, 標高タイル DEM10B), https://maps.gsi.go.jp/development/ichiran.html
- 3DTilesRendererJS (NASA-AMMOS, Apache-2.0).
- HDRI "Pretoria Gardens" by Poly Haven, CC0.
- Colour references (not shipped in the scene): GSI aerial photo (国土地理院); Wikimedia Commons photos by Zairon (CC BY-SA 4.0), Falbisoner (CC BY-SA 4.0), そらみみ (CC BY-SA 3.0), ccfarmer (CC BY 3.0), hagat (CC0).
- three.js (MIT) via CDN.

## iPhone / 가벼운 모드 (light profile)
- Selected automatically on iOS, Android/mobile and low-memory devices; force with `?lite=1`, force the full desktop pipeline with `?full=1`.
- Light profile: OSM buildings only (PLATEAU streaming off; `?tiles=1` to opt in, not recommended on phones), reduced building set beyond 1.4 km, 2048/1024 px aerial photos, indexed half-float geometry with CPU copies freed after GPU upload, FXAA instead of MSAA, pixel ratio ≤ 1.5, 8-bit sRGB canvas, 1024 shadow map, no planar moat reflection, 6-sample SSAO, no bloom.
- Loading progress bar, WebGL context-loss / error fallback screen with a "가벼운 모드로 다시 열기" button.

## 1 km core (phone profile, 2026-11-14)
- Phones load a local, pre-built package of PLATEAU LOD2 buildings within 1 km of the castle (`plateau1k/`, 32 tiles): downloaded once from the PLATEAU CMS, transformed to the local frame, clipped per building to r ≤ 1 km, textures downscaled offline from 8192 px to 2048 px and encoded as KTX2/Basis ETC1S, geometry Draco-compressed. No 8192 px image is ever decoded on the device.
- Sharper ground photo for the core: GSI seamlessphoto z18, ±1.1 km at 4096 px (`aerial_core.jpg` desktop, `aerial_core.ktx2` phones).
- Outside 1 km on phones: aerial photo + DEM mountains + simple flat-roofed OSM buildings ≥ 70 m²; trees only around the core. Moat reflection restored (quarter resolution).
- Source: 3D都市モデル（Project PLATEAU）京都市（2025年度）, 国土交通省, PLATEAU site policy (CC BY 4.0 compatible). Processing: gltf-transform, KTX-Software (Apache-2.0).
