<script>
    export let type='success';
    export let title = 'Genial!!';
    export let description='Tu tarjeta ha sido de alta satisfactoriamente';
    export let closeModal= false;

    let src = '';
    if(type==='success')     src='img/success.png';
    else if(type==='danger') src='img/error.png';
    else if(type==='info')   src='img/info.png';

    
    const close = ()=>{
        document.getElementById('myModal').classList.add('close')
    }

    const removeClassClose =()=>{
        
    }

   
    


</script>
<style>
    .container{
      position: fixed; /* Stay in place */
        z-index: 1; /* Sit on top */
        padding-top: 100px; /* Location of the box */
        left: 0;
        top: 0;
        width: 100%; /* Full width */
        height: 100%; /* Full height */
        overflow: auto; /* Enable scroll if needed */
        background-color: rgb(0,0,0); /* Fallback color */
        background-color: rgba(0,0,0,0.4); /* Black w/ opacity */
    }
    
    .alert__container{
        
        width: 250px;
        height: 250px;
        margin:0 auto;
        top:25%;
        left:25%;
        background-color: #fff;
        border-radius:10px;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        text-align: center;
        
        
        
    }

    .close{
        display:none;
    }
    .alert__img{
        width:  70px;
        height: 70px;
        margin-top: 10px;
    }
    .alert__title{
        margin-bottom: 0;
    }
    .alert__title,
    .alert__description{
        letter-spacing: 1.25px;
    }

    .btn{
        padding: .375rem .75rem;
        font-size: 1rem;
        line-height: 1.5;
        border-radius: .25rem;
    }

    .btn-success{
        color: #fff;
        background-color: #28a745;
        border-color: #28a745;
    }
    .btn-success:hover {
        color: #fff;
        background-color: #218838;
        border-color: #1e7e34;
    }
    .btn-danger {
        color: #fff;
        background-color: #dc3545;
        border-color: #dc3545;
    }

    .btn-danger:hover {
        color: #fff;
        background-color: #c82333;
        border-color: #bd2130;
    }

    .btn-info {
        color: #fff;
        background-color: #17a2b8;
        border-color: #17a2b8;
    }

    .btn-info:hover {
        color: #fff;
        background-color: #138496;
        border-color: #117a8b;
    }

    @media (min-width:576px ) {
        .alert__container{
            top:30%; 
             left:40%;
             width: 300px;
            height: 300px;  
        }
    }


</style>

<div id="myModal" class="container" 
    class:close={closeModal}
    >
    <div class="alert__container">
        <img {src} alt="" class="alert__img">
        <h3 class="alert__title">{title}</h3>
        <p class="alert__description">{description}</p>
        <button class="btn"
                class:btn-success={type==='success'} 
                class:btn-danger={type==='danger'} 
                class:btn-info={type==='info'} 
                id="myBtn"
                on:click={close}>
            Aceptar
        </button>
    </div>
</div>