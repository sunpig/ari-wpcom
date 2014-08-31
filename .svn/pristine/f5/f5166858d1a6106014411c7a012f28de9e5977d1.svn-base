<?php
/**
 * WordPress.com-specific functions and definitions.
 *
 * This file is centrally included from `wp-content/mu-plugins/wpcom-theme-compat.php`.
 *
 * @package Ari
 */

/**
 * Set a default theme color array.
 *
 * @global array $themecolors
 */
function ari_wpcom_setup() {
	$options          = ari_get_theme_options();
	$first_link_color = strtolower( ltrim( $options['first_link_color'], '#' ) );
	$text_color       = strtolower( ltrim( $options['text_color'], '#' ) );

	if ( 'dark' == $options['color_scheme'] ) {
		$GLOBALS['themecolors'] = array(
			'bg'     => '1b1c1b',
			'border' => '4c4c4c',
			'text'   => $text_color,
			'link'   => $first_link_color,
			'url'    => $first_link_color,
		);
	} else {
		$GLOBALS['themecolors'] = array(
			'bg'     => 'ffffff',
			'border' => '4c4c4c',
			'text'   => $text_color,
			'link'   => $first_link_color,
			'url'    => $first_link_color,
		);
	}

	add_theme_support( 'print-style' );
}
add_action( 'after_setup_theme', 'ari_wpcom_setup' );

/**
 * Dequeue the font script if the blog has WP.com Custom Design.
 */
function ari_dequeue_fonts() {
	if ( class_exists( 'TypekitData' ) && class_exists( 'CustomDesign' ) && CustomDesign::is_upgrade_active() ) {
		$customfonts = TypekitData::get( 'families' );

		if ( $customfonts['site-title']['id'] && $customfonts['headings']['id'] && $customfonts['body-text']['id'] ) {
			wp_dequeue_style( 'ari-droid-sans' );
			wp_dequeue_style( 'ari-droid-serif' );
		}
	}
}
add_action( 'wp_enqueue_scripts', 'ari_dequeue_fonts' );
