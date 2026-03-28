# Entregável 02 

### Funcionalidade 2 - Listar Todas as Consultas


#### Método que lista todas as consultas de todos os pacientes
```java
// Mostra todas as consultas de todos os pacientes
public void listarTodasConsultas() {
    // Itera sobre cada consulta em consultas
    for (Consulta c : consultas) {
        c.exibirDetalhes();
    }
}
```
- [Readme.md](README.md)                                                                                                                                                       
- [Funcionalidade 1](Funcionalidade_1.md)
