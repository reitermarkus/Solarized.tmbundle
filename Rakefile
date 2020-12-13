# frozen_string_literal: true

COLORS = {
  base03: '#002b36',
  base02: '#073642',
  base01: '#586e75',
  base00: '#657b83',
  base0: '#839496',
  base1: '#93a1a1',
  base2: '#eee8d5',
  base3: '#fdf6e3',
  yellow: '#b58900',
  orange: '#cb4b16',
  red: '#dc322f',
  magenta: '#d33682',
  violet: '#6c71c4',
  blue: '#268bd2',
  cyan: '#2aa198',
  green: '#859900',
  invisible1: '#b9beb6', # midpoint between base0 and base base2
  invisible01: '#365963', # midpoint between base00 and base base02
}.freeze

LIGHT_TO_DARK_COLORS = {
  base03: :base3,
  base02: :base2,
  base01: :base1,
  base00: :base0,
  base0: :base00,
  base1: :base01,
  base2: :base02,
  base3: :base03,
  invisible1: :invisible01,
  invisible01: :invisible1,
}.freeze

LIGHT_TO_DARK_IDS = {
  'Solarized (Light)' => 'Solarized (Dark)',
  'theme.light.solarized' => 'theme.dark.solarized',
  '38E819D9-AE02-452F-9231-ECC3B204AFD7' => 'A4299D9B-1DE5-4BC4-87F6-A757E71B1597',
}

LIGHT_THEME = 'Themes/Solarized (Light).tmTheme'
DARK_THEME = 'Themes/Solarized (Dark).tmTheme'

task :default do
  light_theme = File.read(LIGHT_THEME)

  light_theme = light_theme.gsub(/#[0-9a-f]+/i, &:downcase)
  File.write LIGHT_THEME, light_theme

  dark_theme = light_theme.gsub(/(?<:>)[^><]+(?=<)/) { |match| LIGHT_TO_DARK_IDS.fetch(match, match) }
  dark_theme = dark_theme.gsub(/#[0-9a-f]+/i) do |match|
    light_color = COLORS.invert.fetch(match)
    dark_color = LIGHT_TO_DARK_COLORS.fetch(light_color, light_color)

    COLORS.fetch(dark_color)
  end
  File.write DARK_THEME, dark_theme
end
