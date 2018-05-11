-- phpMyAdmin SQL Dump
-- version 3.5.1
-- http://www.phpmyadmin.net
--
-- Servidor: localhost
-- Tiempo de generación: 31-05-2017 a las 08:39:58
-- Versión del servidor: 5.5.24-log
-- Versión de PHP: 5.4.3

SET SQL_MODE="NO_AUTO_VALUE_ON_ZERO";
SET time_zone = "+00:00";


/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8 */;

--
-- Base de datos: `fisiodaw`
--

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `consultas`
--

CREATE TABLE IF NOT EXISTS `consultas` (
  `dni` varchar(9) NOT NULL,
  `sociedad` tinyint(4) NOT NULL,
  `fecha` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  `importe` double NOT NULL,
  `cobrada` tinyint(4) NOT NULL,
  `idFactura` int(11) NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (`idFactura`),
  KEY `dni` (`dni`),
  KEY `sociedad` (`sociedad`),
  KEY `dni_2` (`dni`)
) ENGINE=InnoDB  DEFAULT CHARSET=latin1 AUTO_INCREMENT=5 ;

--
-- Volcado de datos para la tabla `consultas`
--

INSERT INTO `consultas` (`dni`, `sociedad`, `fecha`, `importe`, `cobrada`, `idFactura`) VALUES
('11111111A', 1, '2017-05-26 11:14:23', 25, 0, 1),
('22222222B', 0, '2017-05-16 07:31:00', 35, 1, 2),
('33333333C', 0, '2017-05-26 11:00:00', 35, 1, 3),
('33333333C', 0, '2017-05-30 16:00:00', 35, 0, 4);

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `pacientes`
--

CREATE TABLE IF NOT EXISTS `pacientes` (
  `nombre` varchar(100) NOT NULL,
  `direccion` varchar(100) NOT NULL,
  `telefono` varchar(9) NOT NULL,
  `dni` varchar(9) NOT NULL,
  `sociedad` varchar(50) DEFAULT NULL,
  `npoliza` varchar(25) DEFAULT NULL,
  PRIMARY KEY (`dni`),
  UNIQUE KEY `npoliza` (`npoliza`),
  KEY `sociedad` (`sociedad`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

--
-- Volcado de datos para la tabla `pacientes`
--

INSERT INTO `pacientes` (`nombre`, `direccion`, `telefono`, `dni`, `sociedad`, `npoliza`) VALUES
('Rosa Rodríguez García', 'calle San Benito, 6', '644332233', '11111111A', 'SANITAS', '1003'),
('José Pérez López', 'calle Bravo Murillo, 102', '677889987', '22222222B', NULL, NULL),
('Luisa Sánchez Sánchez', 'Paseo de la Castellana, 332', '644345678', '33333333C', NULL, NULL);

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `sociedades`
--

CREATE TABLE IF NOT EXISTS `sociedades` (
  `nombre` varchar(50) NOT NULL,
  `telefono` varchar(9) NOT NULL,
  `contacto` varchar(100) NOT NULL,
  PRIMARY KEY (`nombre`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

--
-- Volcado de datos para la tabla `sociedades`
--

INSERT INTO `sociedades` (`nombre`, `telefono`, `contacto`) VALUES
('ADESLAS', '916778877', 'Beatriz Rodríguez Pérez'),
('SANITAS', '914565432', 'Rafael Sanz García');

--
-- Restricciones para tablas volcadas
--

--
-- Filtros para la tabla `consultas`
--
ALTER TABLE `consultas`
  ADD CONSTRAINT `consultas_ibfk_1` FOREIGN KEY (`dni`) REFERENCES `pacientes` (`dni`);

--
-- Filtros para la tabla `pacientes`
--
ALTER TABLE `pacientes`
  ADD CONSTRAINT `pacientes_ibfk_1` FOREIGN KEY (`sociedad`) REFERENCES `sociedades` (`nombre`);

/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
