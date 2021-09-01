<script>
  import { fly } from 'svelte/transition';
	let b1;
  let formSection1;
  let formSection2;
  let formState = 1
  let form1 = '';
  let form2 = '';
  let form3 = '';
  let form4 = '';
  let form5 = '';
  
  function formCheck1(){
    if(form1 != '' && form2 != '' && form3 != '' && form4 != ''){
      b1.disabled = false
    }else{
      b1.disabled = true
    }
  }
  function b1click(){
    if(formState == 1){
      formState = 2
    }else{
      formState = 1
    }
  }
  function changer1(elem){
    elem.srcElement.style.height='0'
  }
  function changer2(elem){
    elem.srcElement.style.height='initial'
  }

</script>

<p class="eta">Nous prenons présentements des résercations pour xyz</p>
<form action="POST">
  {#if formState == 1}
	<div class="formSection form1" bind:this={formSection1} in:fly|local="{{x: -5, duration: 500, delay: 500}}" out:fly|local="{{x: 5, duration: 500}}" on:outrostart={(formSection1) => changer1(formSection1)} on:outroend={(formSection1) => changer2(formSection1)}>
		<fieldset>
      <legend>Prénom <span style='color:#ff9d9d'>*</span></legend>
			<input type="text" id="pnom" name="pnom" bind:value={form1} on:input={formCheck1}/>
    </fieldset>
		<fieldset>
      <legend>Nom de famille <span style='color:#ff9d9d'>*</span></legend>
			<input type="text" id="nomf" name="nomf" bind:value={form2} on:input={formCheck1}/>
    </fieldset>
    <fieldset>
      <legend>Nom de famille <span style='color:#ff9d9d'>*</span></legend>
			<input type="text" id="nomf" name="nomf" bind:value={form3} on:input={formCheck1}/>
    </fieldset>
    <fieldset>
      <legend>Nom de famille <span style='color:#ff9d9d'>*</span></legend>
			<input type="text" id="nomf" name="nomf" bind:value={form4} on:input={formCheck1}/>
    </fieldset>
	</div>
  {:else}
	<div class="formSection form2" bind:this={formSection2} in:fly|local="{{x: -5, duration: 500, delay: 500}}" out:fly|local="{{x: 5, duration: 500}}" on:outrostart={(formSection2) => changer1(formSection2)} on:outroend={(formSection2) => changer2(formSection2)}/>
  {/if}
	<div class="boutons">
		<button disabled type="button" bind:this={b1} on:click={b1click}>{formState == 1 ? 'Continuer':'Précédent' }</button>
		<button disabled>Envoyer</button>
	</div>
</form>

<style lang="scss">
  @media (max-width: 1024px) {
    
  }
  @media (min-width: 1025px) {
    form, p{
      margin-right: 3rem;
      margin-top: 1rem;
    }
  }
  fieldset{
    margin-inline-start: 0px;
    margin-inline-end: 0px;
    padding-inline-start: 1rem;
    margin-bottom: 0.5rem;
  }
  input{
    width: 100%;
    padding-inline-start: 0.5rem;
    background-color: #252527;
    border: none;
    font-weight: 700;
  }
  legend{
    padding-inline-start: 0.5rem;
    padding-inline-end: 0.5rem;
  }
  button{
    color: black;
    font-weight: 700;
    background-color: white;
    border: none;
    padding: 0.5rem 1rem;
    &:disabled{
      opacity: 0.3;
    }
    &:nth-of-type(2){
      margin-left: 1rem;
    }
  }
  .form2{
    width: 100%;
    height: 16.25rem;
    background-color: red;
  }
</style>
