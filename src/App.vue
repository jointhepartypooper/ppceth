<template>
  <div id="app">
    <router-view/>
  </div>
</template>
 
 <<style lang="scss">
 .layout-dark {
  height: 1000px;
  background: #475d62 url(../src/assets/star-sky.jpg);
  background-size: cover;
  position: relative;
}
 
.layout-dark-form {
  max-width: 620px;
  width: 90%;
  background-color: #1e2833;
  padding: 40px;
  border-radius: 4px;
  transform: translate(-50%, -50%);
  position: absolute;
  top: 50%;
  left: 50%;
  color: #fff;
  box-shadow: 3px 3px 4px rgba(0, 0, 0, 0.2);
}

.layout-dark-form .form-control {
  background: none;
  border: none;
  border-bottom: 1px solid #434a52;
  border-radius: 0;
  box-shadow: none;
  outline: none;
  color: inherit;
}

.layout-dark-form .btn-primary {
  background: #214a80;
  border: none;
  border-radius: 4px;
  padding: 11px;
  box-shadow: none;
  margin-top: 26px;
  text-shadow: none;
  outline: none;
}

.layout-dark-form .btn-primary:hover,
.layout-dark-form .btn-primary:active {
  background: #214a80;
  outline: none;
}

.layout-dark-form .forgot {
  display: block;
  text-align: center;
  font-size: 12px;
  color: #6f7a85;
  opacity: 0.9;
  text-decoration: none;
}

.layout-dark-form .forgot:hover,
.layout-dark-form .forgot:active {
  opacity: 1;
  text-decoration: none;
}

.layout-dark-form .btn-primary:active {
  transform: translateY(1px);
}
 </style>