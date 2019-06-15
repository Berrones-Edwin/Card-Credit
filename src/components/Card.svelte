<script>
    import Alert from './Alert.svelte';
    import Modal from './Modal.svelte';

    let numberCard ='';
    let nameCard='';
    let monthCard='';
    let yearCard='';
    let cvvCard='';
    let validateForm=true;
    let src = '';
    let firstNumber='';

    // Alert
    const alertProops={
        title:'',
        description:'',
        type:'',
        closeModal:true,
        src:''
    }

    let months=['02','03','04','05','06','07','08','09','10','11','12'];

    // Validations
    let numberCardValidate =false;
    let nameCardValidate=false;
    let monthCardValidate=false;
    let monthCardValidate2=false;
    let yearCardValidate=false;
    let cvvCardValidate=false;

    const changeLogo = () =>{
        firstNumber = numberCard.slice(0,1);
        
        if(Number(firstNumber)===3){
           src ='img/american.png';
           
        } else  if(Number(firstNumber)===4){
            src ='img/visa.png';
            
        }else  if(Number(firstNumber)===5){
            src ='img/master.png';
           
        } else{
            src ='';

        }
    }

    const onlyNumber = (myInput) =>{
        if(myInput.length ===0 || myInput==='') return; 

        if(!myInput.match(/^\d+/))
        {

            document.getElementById('myModal').classList.remove('close');

            alertProops.title='Error';
            alertProops.description='Solo se permiten números';
            alertProops.type='danger';
            alertProops.closeModal=false;
            alertProops.src='img/error.png';


            return true;
            
        }
    }

    const formattingNumberCard = () =>{
        changeLogo();
        if(onlyNumber(numberCard)) { 
            numberCard='';
            document.getElementById('numberCard').classList.add('inputInvalid')
        }
        if(numberCard.length===4) numberCard+=' ';
        else if(numberCard.length===9) numberCard+=' ';
        else if(numberCard.length===14) numberCard+=' ';
    }  

    const formattingMonthCard = () =>{

        if(onlyNumber(monthCard)){ 
             monthCard='';
             document.getElementById('monthCard').classList.add('inputInvalid')
        }
      
    }
    const formattingYearCard = () =>{

        if(onlyNumber(yearCard)){
             yearCard='';
             document.getElementById('yearCard').classList.add('inputInvalid')
        }
    }
    const formattingCvvCard = () =>{
        if(onlyNumber(cvvCard)){
            cvvCard='';
            document.getElementById('cvvCard').classList.add('inputInvalid')

        }
    }
    const addCardCredit = (e) =>{

        e.preventDefault();
        if(numberCard.length>0 && nameCard.length>0 && monthCard.length>0 && yearCard.length>0 && cvvCard.length>0){
             numberCard = numberCard.replace(/\s/g, '');

            if(numberCard.length<16){
                numberCardValidate =true;
                return;

            }else if(numberCard.length===16){
               if(isNaN(numberCard)) {
                   numberCardValidate =true;
                    return;
               }
            }
            if(yearCard.length <4 || yearCard.length > 4){
                yearCardValidate=true;
                return;
            }else{
                if(Number(yearCard)< new Date().getFullYear()){
                    yearCardValidate=true;
                    return;
                }
            }
            if(cvvCard.length <3 || cvvCard.length > 3){
                cvvCardValidate=true;
                return;
            }

            numberCardValidate =false;
            nameCardValidate=false;
            monthCardValidate=false;
            yearCardValidate=false;
            cvvCardValidate=false;

            document.getElementById('myModal').classList.remove('close');
            alertProops.title='Correcto';
            alertProops.description='El método de pago se agregó satisfactoriamente';
            alertProops.type='success';
            alertProops.closeModal=false;
            alertProops.src='img/success.png';

        }else{

            if(numberCard === '')
                numberCardValidate =true;
            if(nameCard === '')
                nameCardValidate=true;
            if(monthCard === '')
                monthCardValidate=true;
            if(yearCard === '')
                yearCardValidate=true;
            if(cvvCard === '')
                cvvCardValidate=true;
        }

    }

</script>

<style>
    h2{
        margin: 0;
        padding: 0;
    }
    .title{
        text-align: center;
        margin-top:1rem;
        margin-bottom: 1rem;
        letter-spacing: 2px;

    }
    /*ESTILOS TARJETA*/

    .card-sideLeft{
        height: 200px;
        margin-bottom: 2rem;
    }
    .sideleft__creditCard{
        height: 200px;
        background: #E6DADA; 
        background: -webkit-linear-gradient(to top, #274046, #E6DADA);
        background: linear-gradient(to top, #274046, #E6DADA); 
        width:90%;
        margin:0 auto;
        border-radius: 10px;
        box-shadow: 4px 3px 4px 0px rgb(112, 109, 109);
        color:#FFF;

    }
    .backgroundAmerican{
        background: #2193b0; 
        background: -webkit-linear-gradient(to bottom, #6dd5ed, #2193b0);
        background: linear-gradient(to bottom, #6dd5ed, #2193b0); 

    }
    .backgroundVisa{
        background: #0575E6; 
        background: -webkit-linear-gradient(to left, #021B79, #0575E6);
        background: linear-gradient(to left, #021B79, #0575E6); 


    } 
    .backgroundMaster{
        background: #FF8008; 
        background: -webkit-linear-gradient(to bottom, #FFC837, #FF8008);
        background: linear-gradient(to bottom, #FFC837, #FF8008); 

    }
    .creditCard__container{
        width:100%;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        height:  80px;
    }
    .creditCard__container:nth-child(2){
        display: block;
        
    }
    .creditCard__container:nth-child(2) p {
        letter-spacing: 2px;
        margin-left: 1rem;
        margin-bottom: -0.5rem;
     }

    .creditCard__pin{
        background-color: #dfa73a;
        width: 100px;
        height: 3.5rem;
        border-radius: 10px;
        margin-top:1rem;
        margin-left: 1rem;
        display: grid;
        grid-template-columns: repeat(2,1fr);
        grid-template-rows: repeat(3,1fr);
    }
    .creditCard__pin section{
        width:  20px;
        height: 10px;
        border-radius:2px;
        background-color: #c09133;
        margin:5px auto 0;
    }

    .creditCard__logo{
        width: 60px;
        height:  60px;
        margin-right: 1rem;

    }
    /*ESTILOS FORMULARIO*/
   
    .form__container{
        width: 100%;
        margin-bottom: 1rem;

    }
    .sideRight__form{
        flex-direction: column;
        min-width: 0;
        word-wrap: break-word;
        background-color: #fff;
        background-clip: border-box;
        border: 5px solid rgba(0,0,0,.125);
        border-radius: .25rem;
        padding:10px;

    }
    .sideRight__container{
        border: 5px solid rgba(0,0,0,.125);
        border-bottom:0;
        padding:10px;
        display:flex;
        flex-direction:row;
        justify-content:space-between;
    }
    .sideRight__img{
        width:40px;
        height:40px;
    }
    .sideRight__title{
        color:rgb(78, 76, 76);
        font-weight:normal;
        letter-spacing:2px;
        /* text-align:center; */
    }
    .form__container label,
    .form__container input,
    .form__container select {
        width: 100%;
        
    }
    .form__container label{
        margin-bottom: .5rem;
        letter-spacing: 1px;
    }

    input:focus,
    select:focus,
    option:focus{
        border:none;
        outline: none;
        outline:1px solid #ccc;
    }
    .sideRight__form .btn{
        width: 100%;
        border-radius:10px;
        background-color: #6c757d;
        border-color: #6c757d;
        color:#FFF;
    }
    .sideRight__form .btn:hover{
        color: #fff;
        background-color: #5a6268;
        border-color: #545b62;
    
    }

    @media (min-width:576px ) {
        /* .title{ color:yellow} */

        .card{
            width: 90%;
            margin:0 auto;
            display: flex;
            justify-content: space-around;
            align-items: center;

        }
        .sideleft__creditCard{
            height: 250px;
            width: 400px;
        }
        .creditCard__pin{
            width: 80px;
            height: 60px;
        }

        .creditCard__logo{
            width: 80px;
            height:  70px;
            margin-top: 1rem;

        }
        .creditCard__container:nth-child(1){
            margin-bottom: 4rem;
        }

        /* Formulario */
        
        .form__container:nth-child(3){
            display: flex;
            flex-wrap: wrap;
        }
         .form__container:nth-child(3) label{
             width: 100%;
         }
         .form__container:nth-child(3) input,
         .form__container:nth-child(3) select{
             width: 45%;
             margin-right: 1rem;
             
         }

        /* .alert{
            width:90%;
        } */

    }


    .inputInvalid{
        border:1px solid red;
    }

</style>

<h2 class="title">Nuevo método de pago</h2>


<Modal {...alertProops}  />

<section class="card">
    <div class="card-sideLeft">
       <div class="sideleft__creditCard" 
            class:backgroundAmerican={Number(firstNumber)===3} 
            class:backgroundVisa={Number(firstNumber)===4}
            class:backgroundMaster={Number(firstNumber)===5}
            >

            <div class="creditCard__container">
                <div class="creditCard__pin">
                    <section></section>
                    <section></section>
                    <section></section>
                    <section></section>
                    <section></section>
                    <section></section>
                </div>
                <img {src} class="creditCard__logo" alt="{nameCard}">
            </div>

            <div class="creditCard__container">
                <p>{ numberCard || 'xxxx xxxx xxxx xxxx' }</p>
                <p>{ nameCard || 'Nombre del tarjeta habiente' }</p>
                <p>
                    { monthCard || 'MM' } /
                    { yearCard || 'YYYY' }
                </p>
            </div>
       </div>
    </div>
    <div class="card-sideRight">
        <div class="sideRight__container">
            <h2 class="sideRight__title">Detalles de la Tarjeta</h2>
            <img class="sideRight__img" src="img/master.png" alt="master">
            <img class="sideRight__img" src="img/visa.png" alt="visa">
            <img class="sideRight__img" src="img/american.png" alt="american">
        </div>
        <form action="" class="sideRight__form">

            <!-- Número Pago -->
            <div class="form__container">

                <label for="numberCard">Número de la tarjeta</label>
                <input type="text"
                        placeholder="xxxx xxxx xxxx xxxx"
                        minlength="19" maxlength="19"
                        name="numberCard"
                        bind:value={numberCard}
                        required
                        autocomplete="off"
                        on:keyup={formattingNumberCard}
                        id="numberCard"
                        class:inputInvalid={numberCardValidate}>
                {#if numberCardValidate}
                    <Alert description={'Campo es Invalido. Escriba los 16 digitos de su tarjeta.'} />
                {/if}
            </div>
            <!-- Nombre de la tarjeta -->
            <div class="form__container">

                <label for="nameCard">Nombre del tarjeta habiente</label>
                <input type="text" 
                        name="nameCard"  
                        bind:value={nameCard}
                        required
                        autocomplete="off"
                        placeholder="Nombre del tarjeta habiente "
                        id="nameCard"
                        class:inputInvalid={nameCardValidate}>
                {#if nameCardValidate}
                     <Alert description={'Campo es Invalido.Introuduzca su nombre completo'} />
                {/if}
            </div>
            
            <!-- Fecha Vencimiento -->
            <div class="form__container">

                <label for="monthCard"> Fecha de Vencimiento</label>

                <select id="monthCard" name="monthCard" 
                        bind:value={monthCard} required
                        class:inputInvalid={monthCardValidate} >
                        <option selected value="01">01</option>
                    {#each months as m}
                        <option value="{m}">{m}</option>
                    {/each}
                </select>
                    

                <input type="text" 
                        placeholder="AAAA" 
                        maxlength="4" 
                        minlength="4"
                        name="yearCard"  
                        bind:value={yearCard}
                        pattern="\d*"
                        required
                        autocomplete="off"
                        id="yearCard"
                        on:keyup={formattingYearCard}
                        class:inputInvalid={yearCardValidate}>

            </div>

             {#if monthCardValidate || yearCardValidate }

                <Alert description={'Campo es Invalido.Verifique si el mes  y año son correctos.'} />

            {/if}

             {#if monthCardValidate2}

                <Alert description={'Campo es Invalido. Introduzca un mes válido'} />

            {/if}

            <!-- CVV -->
            <div class="form__container">
                <label for="cvvCard">CVV</label>
                <input type="password" 
                        placeholder="***" 
                        maxlength="3" 
                        minlength="3"
                        name="cvvCard"  
                        bind:value={cvvCard}
                        required
                        autocomplete="off"
                        id="cvvCard"
                        on:keyup={formattingCvvCard}
                        class:inputInvalid={cvvCardValidate}>

                 {#if cvvCardValidate }
                    <Alert description={'Campo es Invalido. Escriba los 3 digitos de su tarjeta.'} />
                {/if}

            </div>
            <button class="btn" on:click={addCardCredit}>
                Agregar Método de pago
            </button>

        </form>
    </div>
</section>
