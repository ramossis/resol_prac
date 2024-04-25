<template>
  <div>
    <div class="container">
      <div class="d-flex d-flex justify-content-center">
        <div class="row">
          <div class="col-4">
            <img
              class="img-thumnail img-fluid rounded-circle"
              src="https://picsum.photos/100/100/?blur"
              alt="logo-cafeteria"
            />
          </div>
          <div class="col-8">
            <h1>CAFETERIA EL BUEN SABOR</h1>
          </div>
        </div>
      </div>

      <nav class="navbar navbar-expand bg-primary" data-bs-theme="dark">
        <div class="container-fluid">
          <a class="navbar-brand" href="#">Navbar</a>
          <button
            class="navbar-toggler"
            type="button"
            data-bs-toggle="collapse"
            data-bs-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent"
            aria-expanded="false"
            aria-label="Toggle navigation"
          >
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
              <li class="nav-item">
                <a class="nav-link active" aria-current="page" href="#">Home</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="#">Link</a>
              </li>
              <li class="nav-item dropdown">
                <a
                  class="nav-link dropdown-toggle"
                  href="#"
                  role="button"
                  data-bs-toggle="dropdown"
                  aria-expanded="false"
                >
                  Dropdown
                </a>
                <ul class="dropdown-menu">
                  <li><a class="dropdown-item" href="#">Action</a></li>
                  <li><a class="dropdown-item" href="#">Another action</a></li>
                  <li><hr class="dropdown-divider" /></li>
                  <li>
                    <a class="dropdown-item" href="#">Something else here</a>
                  </li>
                </ul>
              </li>
              <li class="nav-item">
                <a class="nav-link disabled" aria-disabled="true">Disabled</a>
              </li>
            </ul>
            <form class="d-flex" role="search">
              <input
                class="form-control me-2"
                type="search"
                placeholder="Search"
                aria-label="Search"
              />
              <button class="btn btn-outline-success" type="submit">
                Search
              </button>
            </form>
          </div>
        </div>
      </nav>

      <div class="row">
        <div class="col-6">
            <div>
                <h2 class="text-center" >Lista de Productos de Cafes</h2>
                <table class="table">
            <thead>
              <tr>
                <th scope="col">#</th>
                <th scope="col">Nombre</th>
                <th scope="col">Descripcion</th>
                <th scope="col">Precio</th>
                <th scope="col">Imagen</th>
                <th scope="col">Acciones</th>
              </tr>
            </thead>
            <tbody v-for="item in productos" :key="item.id">
              <tr>
                <th scope="row">{{ item.id }}</th>
                <td>{{ item.nombre }}</td>
                <td>{{ item.descripcion }}</td>
                <td>{{ item.precio }}Bs</td>
                <img
                  class="img-thumbnail img-fluid w-100"
                  :src="scrImg(item.imagen)"
                  alt="img-cafe"
                />
                <td>
                  <button class="btn btn-success" @click="addCart(item.id)">
                    Agregar
                  </button>

                  <button class="btn btn-danger" @click="deleteItem(item.id)">
                    Eliminar
                  </button>
                </td>
              </tr>
            </tbody>
          </table>
            </div>
        
        </div>
        <div class="col-6">
          <div class="d-flex d-flex justify-content-center row">
            <div
              v-for="view in itemCard"
              :key="view.id"
              class=" text-center card"
              style="width: 18rem"
            >
              <img :src="scrImg(view.imagen)" class="card-img-top" alt="..." />
              <div class="card-body">
                <h5 class="card-title">{{ view.nombre }}</h5>
                <p class="card-text">
                  {{ view.descripcion }}
                </p>
                <p class="card-text">{{ view.precio }}Bs.</p>
              </div>
            </div>
          </div>
          <div class="row">
            <h2 class='text-center'>Carrito de Compras</h2>
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">#</th>
                  <th scope="col">Nombre</th>
                  <th scope="col">Descripcion</th>
                  <th scope="col">Imagen</th>
                  <th scope="col">Precio</th>
                </tr>
              </thead>
              <tbody v-for="(subArray,index) in cartPush" :key="index">
                <tr v-for="(item,subIndex) in subArray" :key="subIndex">
                  <th scope="row">{{ item.id }}</th>
                  <td>{{ item.nombre }}</td>
                  <td>{{ item.descripcion }}</td>
                  <img
                  class="img-thumbnail img-fluid w-100"
                  :src="scrImg(item.imagen)"
                  alt="img-cafe"
                />
                  <td>{{ item.precio }}Bs</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style></style>

<script>
import Productos from "@/data/Productos";
export default {
  data() {
    return {
      productos: null,
      itemCard: {},
      cartPush: [],
    };
  },
  mounted() {
    this.onLoad();
  },
  methods: {
    onLoad() {
      this.productos = Productos;
    },
    scrImg(filename) {
      return require("../../public/img/" + filename);
    },
    deleteItem(id) {
      const saved = this.productos.filter((item) => item.id !== id);
      this.productos = [...saved];
    },
    addCart(id) {
      const cart = this.productos.filter((item) => item.id === id);
      this.deleteItem(id);
      this.itemCard = cart;
      this.cartPush.push(cart);
    },
  },
};
</script>
