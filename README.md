from pathlib import Path

# Source file
src = Path("/mnt/data/geography_2000s_ep2.html")
html = src.read_text(encoding="utf-8")

# Replace title and logo text
html = html.replace("GeoFinder 2000", "GeoМытищи 2000")

# Add background image to body (replace existing body background block safely)
import re

pattern = r"body\s*\{[^}]*\}"
replacement = """body{
      margin:0;
      color:#081a33;
      font-family: "Trebuchet MS", Tahoma, Verdana, Arial, sans-serif;
      background: url('Мытищи .webp') no-repeat center center fixed;
      background-size: cover;
    }"""

html = re.sub(pattern, replacement, html, count=1)

# Save updated file
out = Path("/mnt/data/geography_mytishchi_2000.html")
out.write_text(html, encoding="utf-8")

str(out)
