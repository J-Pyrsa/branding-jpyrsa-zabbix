# Branding de Jpyrsa en Zabbx

Este repositorio describe como se debe de implementar el branding de J-Pyrsa en Zabbix, puede servir de base para cualquier otra empresa en la cual se requieran cambiar los colores y logos.

Esta versió sólo aplcara para **Zabbix 7**, si tienes zabbix 6, ver el release zabbix 6, https://github.com/J-Pyrsa/branding-jpyrsa-zabbix/releases/tag/zabbix_6, o bien clona la branch correspondiente.

## Desarrollo

### Pasos preliominares

- Acceder al servidor dónde se tenga Zabbix por medio de la consola
- Una vez en el servidor ejecutar lo siguiente

```bash
cd /var/tmp/
# Clonar este repositorio
git clone https://github.com/J-Pyrsa/branding-jpyrsa-zabbix.git
cd branding-jpyrsa-zabbix
```

> Nota: al momento de clonar el repositorio se podría solicitar las crendenciales del usuario, ya que éste no es público.
>
> TODO: Documentar la parte de la autenticación.

### Cambio de logos predeterminados de Zabbix por logos personalizados

Copiar el archivo PHP de este repositorio `local/conf/brand.conf.php` a `/usr/share/zabbix/local/conf/`

```bash
cp local/conf/brand.conf.php /usr/share/zabbix/local/conf/
```

Contenido del archivo brand.conf.php

```php
<?php
return [
   'BRAND_LOGO' => './images/costum_logo.png', // Logo principal
   'BRAND_LOGO_SIDEBAR' => './images/logo_sidebar.png', // Logo de la barra extendida
   'BRAND_LOGO_SIDEBAR_COMPACT' => './images/logo_compact.png', // logo de la barra compacta
   'BRAND_FOOTER' => 'Jesus , Palma & Romero S.A. de C.V.', // Copyright
   'BRAND_HELP_URL' => 'https://soporte.jpyrsa.net' // Esto ocultará los enlaces a las páginas de soporte de Zabbix y sus integraciones.
];
```

Poner los logos  `costum_logo.png`, `logo_sidebar.png` y `logo_compact.png` en `/usr/share/zabbix/local/conf/`

```bash
mkdir /usr/share/zabbix/rebranding
cp local/conf/*.png /usr/share/zabbix/rebranding/
```

A continuación se muestra el tamaño que debe tener cada logo

- **BRAND_LOGO**: 114x30px
- **BRAND_LOGO_SIDEBAR**: 91x24px
- **BRAND_LOGO_SIDEBAR_COMPACT**: 24x24px

## Asignacón del tema

**Paso 1**: Copiar los archivos `jpyrsa-theme.css` y  `jpyrsa-theme.css` en `assets/styles/`

```bash
cp assets/styles/*.css /usr/share/zabbix/assets/styles/
```

**Paso 2**: Renombrar el archivo /usr/share/zabbix/include/classes/core/APP.php

```bash
cd /usr/share/zabbix/include/classes/core/
cp APP.php APP.php.back
```

**Paso 3**: Agregar 'jpyrsa-theme'=> _('JPYRSA theme'), y 'jpyrsa-dark-theme'=> _('JPYRSA dark theme') dentro de la función getThemes()

Para ello, edita el archivo  `nano APP.php`

```php
class APP extends ZBase {
	public static function getThemes() {
		return array_merge(parent::getThemes(), [
                        // ... aca podría haber más lineas
			'jpyrsa-theme'=> _('JPYRSA theme'),
			'jpyrsa-dark-theme'=> _('JPYRSA dark theme')
		]);
	}
}
```

**Paso 4**: Activar el nuevo tema.

En la interfaz de Zabbix, configurar este tema como predeterminado o cambiar su tema en el perfil de usuario.

![image](https://github.com/J-Pyrsa/branding-jpyrsa-zabbix/assets/30660343/a19e62fa-92ab-4aa7-b99d-343c51d31b63)

¡Disfruta de la nueva apariencia!

## Bibliografía

_8 Creating your own theme._ (s. f.). Zabbix Documentation. Recuperado 26 de abril de 2024, de https://www.zabbix.com/documentation/current/en/manual/web_interface/theming 13 Rebranding. (s. f.). Zabbix _Rebranding_. Recuperado 26 de abril de 2024, de https://www.zabbix.com/documentation/current/en/manual/web_interface/rebranding
- Dmitry Lambert. (2024, 12 noviembre). __How to rebrand Zabbix 7.0 ( Replace logos )__ [Vídeo]. YouTube. https://www.youtube.com/watch?v=fswSA9pC9no
- initMAX s.r.o. (2024b, noviembre 7). __Zabbix Rebranding - InitMAX S.r.o.__ https://www.initmax.com/wiki/zabbix-rebranding/