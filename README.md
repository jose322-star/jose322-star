- 👋 Hi, I’m @jose322-star
Creacion de tablas Ferreteria el Buen Vecino sql

-- Creación de la tabla 'Proveedor'
CREATE TABLE Proveedor (
    proveedor_id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    contacto VARCHAR(100),
    telefono VARCHAR(20),
    direccion VARCHAR(255)
);

-- Creación de la tabla 'Producto'
CREATE TABLE Producto (
    producto_id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    descripcion TEXT,
    precio DECIMAL(10, 2) NOT NULL,
    stock_actual INT NOT NULL,
    proveedor_id INT,
    CONSTRAINT fk_proveedor FOREIGN KEY (proveedor_id) REFERENCES Proveedor(proveedor_id) ON DELETE SET NULL ON UPDATE CASCADE
);

-- Creación de la tabla 'Cliente'
CREATE TABLE Cliente (
    cliente_id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    telefono VARCHAR(20),
    direccion VARCHAR(255)
);

-- Creación de la tabla 'Pedido'
CREATE TABLE Pedido (
    pedido_id INT AUTO_INCREMENT PRIMARY KEY,
    cliente_id INT,
    fecha_pedido DATE NOT NULL,
    estado VARCHAR(50) NOT NULL,
    total DECIMAL(10, 2) NOT NULL,
    CONSTRAINT fk_cliente FOREIGN KEY (cliente_id) REFERENCES Cliente(cliente_id) ON DELETE CASCADE ON UPDATE CASCADE
);

-- Creación de la tabla 'Producto_Pedido' (relación muchos a muchos entre 'Pedido' y 'Producto')
CREATE TABLE Producto_Pedido (
    pedido_id INT,
    producto_id INT,
    cantidad INT NOT NULL,
    precio_unitario DECIMAL(10, 2) NOT NULL,
    PRIMARY KEY (pedido_id, producto_id),
    CONSTRAINT fk_pedido FOREIGN KEY (pedido_id) REFERENCES Pedido(pedido_id) ON DELETE CASCADE ON UPDATE CASCADE,
    CONSTRAINT fk_producto FOREIGN KEY (producto_id) REFERENCES Producto(producto_id) ON DELETE CASCADE ON UPDATE CASCADE
);

-- Datos de ejemplo para Proveedores
INSERT INTO Proveedor (nombre, contacto, telefono, direccion)
VALUES 
('Proveedor A', 'Juan Perez', '123456789', 'Calle Falsa 123'),
('Proveedor B', 'Maria Gomez', '987654321', 'Avenida Siempre Viva 742');

-- Datos de ejemplo para Productos
INSERT INTO Producto (nombre, descripcion, precio, stock_actual, proveedor_id)
VALUES
('Martillo', 'Martillo de acero de 16 oz', 120.00, 50, 1),
('Clavos', 'Clavos de acero de 2 pulgadas', 50.00, 200, 1),
('Destornillador', 'Destornillador de estrella', 75.00, 80, 2);

-- Datos de ejemplo para Clientes
INSERT INTO Cliente (nombre, telefono, direccion)
VALUES
('Cliente A', '5551234', 'Calle 1, Ciudad'),
('Cliente B', '5555678', 'Avenida 2, Ciudad');

-- Datos de ejemplo para Pedidos
INSERT INTO Pedido (cliente_id, fecha_pedido, estado, total)
VALUES
(1, '2024-10-06', 'Pendiente', 300.00),
(2, '2024-10-07', 'Completado', 150.00);

-- Datos de ejemplo para la relación Producto_Pedido (productos en los pedidos)
INSERT INTO Producto_Pedido (pedido_id, producto_id, cantidad, precio_unitario)
VALUES
(1, 1, 2, 120.00), -- Pedido 1 tiene 2 Martillos
(1, 2, 1, 50.00),  -- Pedido 1 tiene 1 Caja de Clavos
(2, 3, 2, 75.00);  -- Pedido 2 tiene 2 Destornilladores

-- Consultas de prueba
SELECT * FROM Proveedor;
SELECT * FROM Producto;
SELECT * FROM Cliente;
SELECT * FROM Pedido;
SELECT * FROM Producto_Pedido;
