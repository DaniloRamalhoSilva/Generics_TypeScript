
<h1>Gabarito</h1>
<details>
  <summary><strong> Exercicio 1 </strong></summary>
  <br>
  <p>Dado o codigo abaixo implemente a funções comparaGeneric de mode que subistutua as funçoes comparaNumber e comparaString<br> 
  obs. o paremetros da função comparaGeneric devem ser tipados e serem do mesmo tipo para que possam ser comparados corretamente.</p>

  ```typescript
    function comparaGeneric<T>(x: T, y: T): boolean {
      if(x !== y) return true;
      return false;
    }
  ```
</details>
<details>
  <summary><strong> Exercicio 2 </strong></summary>
  <br>
  <p>Dado o codigo abaixo refetore a interface IDataId  e a função filterById
  de modo que a função possa filtra ids do tipo string ou do tipo number;
  dica: lembrese do conceito de Type Constraints </p>

  ```typescript
    interface IDataId<T extends string | number> {
      id: T;
      nome: string;
    }

    const filterById =<T> (id: T , data: IDataId<T>[] ) => {
    return data.filter((d) => id === d.id);
    }
  ```

</details>
<details>
  <summary><strong> Exercicio 3 </strong></summary>
  <br>
  <p>Sugestão de resposta para o exercicio</p>

  ```typescript
    const produtos = [
      {id: "7891", nome: "bola"}, 
      {id: "7892", nome: "carro"}, 
      {id: "7893", nome: "Pipa"}, 
      {id: "7892", nome: "boneca"}
    ]

    const clientes = [
      {id: 1, nome: "Maria"}, 
      {id: 2, nome: "João"}, 
      {id: 10, nome: "Pedro"}, 
      {id: 11, nome: "Larisa"},
    ];

    interface IDataBase<T extends string | number> {
      id?: T;
      nome: string;
    }

    class ClassBase <T extends string | number>{

      constructor(private data: IDataBase<T>[]){};

      public create = (entity: IDataBase<T>) => {
        this.data.push(entity);
        return this.getAll();
      }

      public getById = (id: T) => {
        return this.data.filter((d) => id === d.id )[0];
      }

      public getAll = () => {
        return this.data;
      }

      public delete = (id: T) => {
        this.data = this.data.filter((d) => id !== d.id );
        return this.getAll();
      }

      public update = (id: T, entity: IDataBase<T>) => {
        this.delete(id);
        this.data.push(entity);
        return this.getAll();
      }
    }

    class Cliente extends ClassBase<number> {
      constructor(){
        super(clientes);    
      }
    }

    class Produto extends ClassBase<string> {
      constructor(){
        super(produtos);    
      }
    }

    const myCliente = new Cliente();
    const myProduct = new Produto();

    console.log(myCliente.getAll());
    console.log(myCliente.getById(1));
    console.log(myCliente.create({id: 21, nome: 'Fabilo'}));
    console.log(myCliente.delete(1));
    console.log(myCliente.update(21, {id: 21, nome: 'Fabio'}));

    console.log(myProduct.getAll());
    console.log(myProduct.getById("7891"));
    console.log(myProduct.create({id: "7899", nome: 'xadres'}));
    console.log(myProduct.delete("7891"));
    console.log(myProduct.update("7899", {id: "7899", nome: 'Jogo de xadres'}));
  ```
  
</details>





2. 



const filterById = <T extends string | number >(id: T , data: IDataId<T>[] ) => {
  return data.filter((d) => id === d.id);
}