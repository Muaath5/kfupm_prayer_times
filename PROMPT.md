# Comprehensive Prompt for KFUPM Prayer Times Web Application

Create a single-page web application for displaying Islamic prayer times for King Fahd University of Petroleum and Minerals (KFUPM) in Dhahran, Saudi Arabia.

## Technical Requirements

### Prayer Time Calculations
- Use the **PrayTimes.js library** (version 2.3) embedded directly in the HTML file (no external requests)
- Calculation method: **Makkah (Umm Al-Qura)** - the official method for Saudi Arabia
- Coordinates: **26°18'49.4"N, 50°08'46.1"E** (26.3137222, 50.1461389)
- Timezone: UTC+3 (Saudi Arabia)
- Prayer times: Fajr, Dhuhr (Jumaa on Fridays), Asr, Maghrib, Isha
- Include Iqama times with customizable delays for each prayer (defaults: Fajr 30min, Dhuhr 20min, Asr 20min, Maghrib 15min, Isha 20min)
- Display note: "مسجد علي بن أبي طالب" (Ali Ibn Abi Talib Mosque)

### Design & Branding
- **KFUPM Color Scheme** (use CSS variables):
  - Primary: #008540
  - Secondary: #00573F
  - Tertiary: #003E51
  - Gold: #DAC961
  - Dark Gold: #AA8A00
  - Light Gray: #D9DAE4
  - Dark Gray: #373938
- **Font**: IBM Plex Sans Arabic (load from Google Fonts)
  - Regular (400) for body text
  - Bold (700) for titles and headings
- **Logo**: Use `/kfupm_logo.svg` as both header image and favicon
- Mobile-responsive, clean design with no animations
- Fast loading, no scrolling required on mobile/desktop (except advanced view)

### Main Interface

**Header Section** (green background):
- KFUPM logo centered
- Small text: "مسجد علي بن أبي طالب"
- Date display: Gregorian and Hijri (use browser's `Intl.DateTimeFormat` with `'ar-SA-u-ca-islamic'` calendar)
- Three info boxes showing:
  - Current time (with seconds, 12/24hr format with ص/م or AM/PM)
  - Time remaining until next Athan (بقي للأذان)
  - Time remaining until next Iqama (بقي للإقامة)

**Control Buttons**:
- Language toggle (Arabic ⟷ English with RTL/LTR direction change)
- Advanced view toggle
- Settings toggle (with ▼/▲ arrow indicator)
- All buttons same color (primary green)

**Prayer Table**:
- Three columns: Prayer Name | Athan Time | Iqama Time
- Highlight the **next upcoming prayer** with gold background (#DAC961)
- Bold text for highlighted row
- On Fridays, show "الجمعة" instead of "الظهر"

### Advanced View (Collapsible)
Display:
- Sunrise time (الشروق / Sunrise)
- Day length (طول النهار / Day Length) - duration from sunrise to maghrib
- Night length (طول الليل / Night Length) - 24h minus day length
- Midnight (منتصف الليل / Midnight)
- Last third of night begins (بداية الثلث الأخير / Last Third)
- Sahar begins (بداية السحر (السدس الأخير) / Sahar (Last Sixth)) - last 1/6 of night

All durations should include units with proper formatting.

### Settings Panel (Collapsible)
- Time format selector: 12-hour (default) or 24-hour
- Iqama delay inputs for each of the 5 prayers (in minutes)
- Compact grid layout (2-3 columns on mobile, more on desktop)
- Labels shortened: "الفجر (د)" instead of full text
- Close button (X) in top-right corner
- Save all settings to cookies for persistence

### Time Display Logic

**Next Prayer Tracking**:
- If current time < Athan time: Show countdown to both Athan and Iqama
- If current time >= Athan AND < Iqama: Show "--:--" for Athan, countdown to Iqama only
- If all prayers passed: Show countdown to tomorrow's Fajr

**Time Formatting**:
- 12-hour format: Use ص (morning) and م (afternoon) in Arabic, AM/PM in English
- Support both 12h and 24h formats throughout

**Duration Formatting in Arabic** (critical):
Create a separate function with proper Arabic plural rules:
- 1: ساعة / دقيقة (singular)
- 2: ساعتان / دقيقتان (dual)
- 3-10: ساعات / دقائق (plural)
- 11+: ساعة / دقيقة (singular for 11+)
- When showing both hours and minutes, use "و" between them
- Example: "ساعتان و 15 دقيقة"

### Localization
Full bilingual support (Arabic/English):
- Default: Arabic (RTL)
- Toggle updates all text, including:
  - UI labels
  - Prayer names
  - Month names
  - Duration units
  - Date formats
- Persist language preference in cookies

### Data Persistence
Store in cookies (1-year expiration):
- Selected language
- Time format preference (12h/24h)
- Custom Iqama times for all prayers

### SEO & Meta Tags
Include:
- Meta description (bilingual)
- Keywords (prayer times, KFUPM, Dhahran, Saudi Arabia)
- Open Graph tags
- Twitter Card tags
- Favicon reference
- Robots meta tag

### Performance Requirements
- Single HTML file (all CSS and JavaScript embedded)
- No external dependencies except:
  - Google Fonts (IBM Plex Sans Arabic)
  - Logo file (/kfupm_logo.svg)
- Update display every second
- Fast, no loading delays

### Code Structure
1. Embed complete PrayTimes.js library code (copy verbatim from praytimes.org)
2. Separate the PrayTimes functions from custom application logic
3. Use CSS variables for the color scheme
4. Clean, maintainable JavaScript
5. Responsive CSS with mobile-first approach

### Important Notes
- Prayer times must be accurate for KFUPM's exact coordinates
- Use Makkah calculation method (NOT MWL or others)
- Hijri date must use browser API to avoid contradictions with actual Islamic calendar
- No easter eggs or hidden features
- Professional, clean appearance suitable for university environment
- Compact layout - everything visible without scrolling (except advanced section)
