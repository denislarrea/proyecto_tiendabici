<template>
  <div>
    <footer style="background-color: #deded5;">
      <div class="container p-4">
        <div class="row">
          <div class="col-lg-4 col-md-12 mb-4">
            <h5 class="mb-3" style="letter-spacing: 2px; color: #818963;">Contactenos</h5>
            <p class="footer__text">
              Direccion: Jacinto Rios 321<br>
              Ciudad: Córdoba<br>
              CP: 5000<br>
              Tel: 035145565656<br>
              Fax: 156532322<br>
              Email: denisbikeshop@hotmail.com
            </p>
          </div>
          <div class="col-lg-4 col-md-6 mb-4">
            <h5 class="mb-3" style="letter-spacing: 2px; color: #818963;">Medios de Pago</h5>
            <div class="center__img-container">
              <img src="../assets/images/mediosdepago.png" class="center__img" alt="medios de pago">
            </div>
          </div>
          <div class="col-lg-4 col-md-6 mb-4">
            <h5 class="mb-1" style="letter-spacing: 2px; color: #818963;">Redes Sociales</h5>
            <div class="icons">
              <b-icon icon="instagram" class="social-icon"></b-icon>
              <b-icon icon="Facebook" class="social-icon"></b-icon>
              <b-icon icon="Twitter" class="social-icon"></b-icon>
            </div>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  name: "FooterComponent",
};
</script>

<style scoped>
.footer {
  color: white;
}

.footer__text {
  text-align: center;
  color: #7C081A;
}

.center__img-container {
  display: flex;
  justify-content: center;
}

.center__img {
  width: 200px;
  height: 90px;
  transition: transform 0.3s;
}

.center__img:hover {
  transform: scale(1.15);
}

h5 {
  text-align: center;
  color: #7C081A;
}

.icons {
  display: flex;
  justify-content: center;
}

.social-icon {
  font-size: 50px;
  margin: 5px;
}
</style>
