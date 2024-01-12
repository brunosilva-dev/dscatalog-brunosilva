# JAVA (SPRING/MAVEN)

> Criando um projeto do zero

- Utilizar o Spring Initialzer

> Dicas para iniciar o projeto

- Toda vez que for iniciar um projeto MVC, sempre começar por onde não tem vínculo a outros packages, como por exemplo uma categoria de produto. A categoria do produto não é dependente de nenhum produto para ser criada, porém o produto sim depende de ao menos uma categoria para existir.

- Quando cor criar uma entidade sempre colocar como private e depois criar o getter e setter

- Iniciar um método publico dentro da classe também

- Iniciar um construtor para ser acionado futuramente caso precise

- Criar hashcode and equals para o id, pois, ele vai fazer um comparativo dos id's para que não se repita

- Colocar o implements Serializable também no método principal. É um padrão o java para converter em bytes

```java
// Exemplo
public class Category implements Serializable {

	private static final long serialVersionUID = 1L;
	private Long id;
	private String name;

	public Category() {

	}

	public Category(Long id, String name) {
		super();
		this.id = id;
		this.name = name;
	}

	public Long getId() {
		return id;
	}

	public void setId(Long id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	@Override
	public int hashCode() {
		return Objects.hash(id);
	}

	@Override
	public boolean equals(Object obj) {
		if (this == obj)
			return true;
		if (obj == null)
			return false;
		if (getClass() != obj.getClass())
			return false;
		Category other = (Category) obj;
		return Objects.equals(id, other.id);
	}

}
```

> Criando recursos REST para disponibilizar ao sistema

- Toda vez que for criar o recurso e ele tiver vinculo com alguma entidade, colocar o nome e o package (CategoryResource)

- Quando for criar o recursos como rest, sempre colocar a annotation @RestController
	- A Anotation serve para usar algo que já está implementado
	
- Colocar também a annotation @RequestMapping(value = "/informarOCaminho")

- Para colocar que é o método é um endpoint, é preciso que coloque a annotation @GetMapping

```java
@RestController
@RequestMapping(value = "/categories")
public class CategoryResource {

	@GetMapping
	public ResponseEntity<List<Category>> findAll() {
		List<Category> list = new ArrayList<>();
		list.add(new Category(1L, "Books"));
		list.add(new Category(2L, "Electronics"));

		return ResponseEntity.ok().body(list);
	}
}
```

