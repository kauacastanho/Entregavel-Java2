# Entregável 02 - Sistema de Gestão de Pacientes e Consultas


## Funcionalidades à serem implementadas
- [Desmarcar consulta](Funcionalidade_1.md)
  - Permite cancelar uma consulta já agendada, removendo ela da lista de consultas do sistema
    
- [Listar todas as consultas marcadas](Funcionalidade_2.md)
  - Exibe todas as consultas cadastradas no sistema com informações do paciente, médico, data, horário e especialidade

- Remarcar Consulta
  - Permite alterar a data e/ou horário de uma consulta existente, mantendo o mesmo paciente, médico e especialidade

- validar a Entrada do usuário
  - Validar a resposta do usuário para verificar se os dados digitados (CPF, nome, data, telefone, etc.) estão no formato correto e não estão vazios ou inválidos.

- Cadastro de médicos
  - Permite cadastrar médicos no sistema com informações como nome e especialidade para que possam ser vinculados às consultas

- Ordernar consultas por data e horário
  - Organiza a lista de consultas em ordem cronológica, mostrando primeiro as consultas mais próximas e depois as mais distantes


### Código Completo
###### Cadastros Automáticos - Linha 144

```java
import java.util.ArrayList;
import java.util.Scanner;

class Paciente {
    private String nome;
    private String cpf;
    private int idade;
    private String telefone;

    public Paciente(String nome, String cpf, int idade, String telefone) {
        this.nome = nome;
        this.cpf = cpf;
        this.idade = idade;
        this.telefone = telefone;
    }

    public String getCpf() {
        return cpf;
    }

    public void exibirInformacoes() {
        System.out.println("Paciente: " + nome + " | CPF: " + cpf + " | Idade: " + idade + " | Telefone: " + telefone);
    }
}

class Consulta {
    private Paciente paciente;
    private String data;
    private String horario;
    private String especialidade;
    private String medico;

    public Consulta(Paciente paciente, String data, String horario, String especialidade, String medico) {
        this.paciente = paciente;
        this.data = data;
        this.horario = horario;
        this.especialidade = especialidade;
        this.medico = medico;
    }


    public String getCpfPaciente() {
        return paciente.getCpf();
    }
    // Pega a data da consulta
    public String getData() { 
        return data; 
    }
    // Pega o horário da consulta
    public String getHorario() { 
        return horario; 
    }

    public void exibirDetalhes() {
        System.out.println("Consulta com " + medico + " | Especialidade: " + especialidade +
                " | Data: " + data + " | Horário: " + horario);
        paciente.exibirInformacoes();
    }
}

class SistemaHospital {
    private ArrayList<Paciente> pacientes = new ArrayList<>();
    private ArrayList<Consulta> consultas = new ArrayList<>();

    public void cadastrarPaciente(String nome, String cpf, int idade, String telefone) {
        pacientes.add(new Paciente(nome, cpf, idade, telefone));
        System.out.println("Paciente cadastrado com sucesso!");
    }

    public void agendarConsulta(String cpf, String data, String horario, String especialidade, String medico) {
        Paciente pacienteEncontrado = null;
        for (Paciente p : pacientes) {
            if (p.getCpf().equals(cpf)) {
                pacienteEncontrado = p;
                break;
            }
        }
        if (pacienteEncontrado != null) {
            consultas.add(new Consulta(pacienteEncontrado, data, horario, especialidade, medico));
            System.out.println("Consulta agendada com sucesso!");
        } else {
            System.out.println("Paciente não encontrado!");
        }

    }

    // Mostra todas as consultas de todos os pacientes
    public void listarTodasConsultas() {
        // Itera sobre cada consulta em consultas
        for (Consulta c : consultas) {
            c.exibirDetalhes();
        }
    }

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

    public void listarConsultasPaciente(String cpf) {
        boolean encontrou = false;
        for (Consulta c : consultas) {
            if (c.getCpfPaciente().equals(cpf)) {
                c.exibirDetalhes();
                encontrou = true;
            }
        }
        if (!encontrou) {
            System.out.println("Nenhuma consulta encontrada para este CPF.");
        }
    }
}

public class App {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        SistemaHospital sistema = new SistemaHospital();

        
        // CADASTROS AUTOMÁTICOS PARA TESTE
        SistemaHospital sistema_teste = new SistemaHospital();
        sistema_teste.cadastrarPaciente("João Silva", "111", 30, "9999-1111");
        sistema_teste.cadastrarPaciente("Maria Souza", "222", 25, "9999-2222");

        sistema_teste.agendarConsulta("111", "20", "10:00", "Cardiologia", "Dr. Carlos");
        sistema_teste.agendarConsulta("222", "21", "14:00", "Pediatria", "Dra. Ana");

        while (true) {
            System.out.println("\nMenu:");
            System.out.println("1 - Cadastrar Paciente");
            System.out.println("2 - Agendar Consulta");
            System.out.println("3 - Listar Consultas de um Paciente");
            System.out.println("4 - Desmarcar consulta");
            System.out.println("5 - Listar Todas as Consultas");
            System.out.println("6 - Sair");
            System.out.print("Escolha uma opção: ");

            int opcao = scanner.nextInt();
            scanner.nextLine();

            if (opcao == 1) {
                System.out.print("Nome: ");
                String nome = scanner.nextLine();
                System.out.print("CPF: ");
                String cpf = scanner.nextLine();
                System.out.print("Idade: ");
                int idade = scanner.nextInt();
                scanner.nextLine();
                System.out.print("Telefone: ");
                String telefone = scanner.nextLine();
                sistema.cadastrarPaciente(nome, cpf, idade, telefone);

            } else if (opcao == 2) {
                System.out.print("CPF do paciente: ");
                String cpf = scanner.nextLine();
                System.out.print("Data (dd/mm/aaaa): ");
                String data = scanner.nextLine();
                System.out.print("Horário (hh:mm): ");
                String horario = scanner.nextLine();
                System.out.print("Especialidade: ");
                String especialidade = scanner.nextLine();
                System.out.print("Médico: ");
                String medico = scanner.nextLine();
                sistema.agendarConsulta(cpf, data, horario, especialidade, medico);

            } else if (opcao == 3) {
                System.out.print("CPF do paciente: ");
                String cpf = scanner.nextLine();
                sistema.listarConsultasPaciente(cpf);
                
            } else if (opcao == 4) {
                System.out.print("CPF do paciente: ");
                String cpf = scanner.nextLine();
                System.out.print("Data (dd/mm/aaaa): ");
                String data = scanner.nextLine();
                System.out.print("Horário (hh:mm): ");
                String horario = scanner.nextLine();
                sistema.desmarcarConsulta(cpf, data, horario);
            
            } else if (opcao == 5) {
                sistema.listarTodasConsultas();

            } else if (opcao == 6) {
                System.out.println("Saindo...");
                break;
            } else {
                System.out.println("Opção inválida! Tente novamente.");
            }
        }
        scanner.close();
    }
}
```
