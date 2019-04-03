# Prova2

- Projeto: Projeto de rede social que permite que o usuário com conta tenha uma sistema de amigos, comunidades, e mensagens com outros usuário. 

- Padrão 1: Proxy
	- Motivação: Criar um substituto para uma classe para ocorrer um acesso indireto a mesma, criando uma nova camada de proteção.
	- Solução: O usuário só poderá acessar a classe User e seus métodos quando tiver a devida permissão de acesso após passar por uma verificação proposta pelo Proxy.

- Padrão 2: Iterator
	- Motivação: Acesso de modo sequencial aos Maps e Listas implementados quando necessário sem ter a necessidade de expor sua estrutura interna.
	- Solução: Utilizado em diversos métodos para melhor iteração em lista e maps, suportando vários percursos e mantendo controle.


- Classes e métodos afetados pelos Padrões:
	- Proxy:
		- MainSystem: A verificação de permissão não será mais feita por essa classe na main e ao criar um novo usuário é feito um novo tipo UserProxy. 
		- User: O modo de instaciar o objeto User foi afetado, já que agora é preciso passar pelo Proxy para se ter qualquer referência associada a classe original, então o acesso para cada método implementado que necessita do User agora é feita por uma chamada na classe Proxy quando permitido.
		- Messages: Só pode ter acesso garantido quando associada ao User, logo está associada ao Proxy.
		- Requests: Análogo a classe Messages.
		- Classes adicionadas:
		  - UserProxyInterface: Interface que irá associar a classe Proxy com a classe original.  
		  - UserProxy: Substituto da classe original e também onde é checada a permissão para o acesso pelo método authenticate.
	- Iterator:
		- MainSystem: Em partes onde ocorre iterações sequenciais nos Maps agora se usa um Iterator.
		- UserProxy: No método de autenticação é necessária uma iteração no Map users para haver a permissão.
		- User: Métodos como NewUser, EditProfile e RemoveAccount vão precisar iterar em Maps e ArrayLists.
		- Community: A iteração ocorre em quase todos os métodos da classe por meio dos métodos de Iterator.
		- Classes Adicionadas:
			- IteratorInterface: Interface necessária para a implementação do Iterator.
			- Iterator: É onde ocorre as iterações.
