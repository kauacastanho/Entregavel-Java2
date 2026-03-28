# Entregável 02 

### Funcionalidade 1 - Remover Consulta


#### Retornando data e horário com str
```java
// Pega a data da consulta
public String getData() { 
    return data; 
}
// Pega o horário da consulta
public String getHorario() { 
    return horario; 
}
```
#### Método desmarcarConsulta
```java
// Criando o método que recebe o cpf, data e horario da consulta e remove a consulta da lista
public void desmarcarConsulta(String cpf, String data, String horario) {
    
    Consulta remover = null;

    // Itera sobre cada consulta da lista consultas
    for (Consulta c : consultas) {
        // Compara o cpf
        if (c.getCpfPaciente().equals(cpf) &&
            // Compara a data
            c.getData().equals(data) &&
            // Compara o horario
            c.getHorario().equals(horario)) {
            // Se o existir alguma consulta no cpf, guarda a consulta na variavel remover
            remover = c;
            break;  
        }
    }
    // Verifica se encontrou alguma consulta
    if (remover != null) {
        // Remove a consulta
        consultas.remove(remover);
        System.out.println("Consulta desmarcada com sucesso!");
    } else {
        System.out.println("Consulta não encontrada!");
    }
}
```
- [Readme.md](README.md)                                                                                                                                                       
- [Funcionalidade 2](Funcionalidade_2.md)
