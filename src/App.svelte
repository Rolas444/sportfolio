<script lang="ts">
  import en from "./assets/en.json";
  import es from "./assets/es.json";
  import fs from "fs";
  import "@fortawesome/fontawesome-free";
    import { each } from "svelte/internal";
  interface pinfo {
    name: string;
    headline: string;
    resume: string;
    contact: {
      email: string;
      phone: string;
      place: string;
    };
    links: {
      linkedin: string;
      github: string;
      twitter: string;
      portfolio: string;
      docker: string;
    };
    techskills: string[];
    softskills: string[];
    languages: string[];
    expirience: [
      {
        title: string;
        desc: string[];
        lapse: string;
      }
    ];
    education: [
      {
        title: string;
        inst: string;
        lapse: string;
      }
    ];
  }

  let lang: boolean = true;
  // alert(en.name) ;
  var datacv: any = lang ? en : es;
  var theme = false;

  let taghtml = document.getElementsByTagName("html");

  const changeTheme = (e) => {
    e.preventDefault();
    theme = !theme;
    if (theme) taghtml[0].setAttribute("data-theme", "light");
    else taghtml[0].setAttribute("data-theme", "dark");
  };

  const changeLang = (e) => {
    e.preventDefault();
    lang = !lang;
    datacv = lang ? en : es;
  };
</script>

<nav class="container-fluid">
  <ul />
  <ul />
  <ul>
    <li>
      <a
        role="button"
        target="_blank"
        href="https://drive.google.com/drive/folders/1xL0TgH32Tt1PUs_cPBhDnXXrdElDMkAr?usp=sharing"
        class="switcher contrast"><i class="bi bi-file-earmark-arrow-down" /></a
      >
    </li>
    <li>
      <button on:click={changeLang} class="switcher contrast"
        ><i class="bi bi-translate" /></button
      >
    </li>
    <li>
      <button on:click={changeTheme} class="switcher contrast"
        ><i class="bi bi-lightbulb" /></button
      >
    </li>
  </ul>
</nav>

<section class="container">
  <nav>
    <ul />
    <ul>
      <li>
        <hgroup>
          <h1><strong>{datacv.name}</strong></h1>
          <h2 class="center">{datacv.headline}</h2>
        </hgroup>
      </li>
    </ul>
    <ul />
  </nav>
</section>
<section>
  <div>
    <h5 class="container"><i><em><cite>{datacv.resume}</cite></em></i></h5>
  </div>
  <nav class="container">
    <ul class="row row-cols-auto">
      <li class="col">
        <a><i class="bi bi-envelope-at" /> {datacv.contact.email}</a>
      </li>
      <li class="col">
        <a href="https://wa.me/51943808616?text='Hi, Rolando'" target="_blank"
          ><i class="bi bi-whatsapp" /> {datacv.contact.phone}</a
        >
      </li>
      <li class="col">
        <a><i class="bi bi-geo-alt-fill" /> {datacv.contact.place}</a>
      </li>
    </ul>
  </nav>
</section>

<!-- <section>
  <h5 class="center"><strong>Tech Skills <i class="bi bi-tools" /></strong></h5>
  <div class="container ">
    <ul class="row">
      {#each datacv.techskills as i}
        <lo class="col"><ins>{i}</ins></lo>
      {/each}
    </ul>
  </div>
</section>
<section>
  <h5 class="center">
    <strong>Soft Skills <i class="bi bi-people-fill" /></strong>
  </h5>
  <div class="container ">
    <ul class="row">
      {#each datacv.softskills as i}
        <lo class="col"><ins><i>{i}</i></ins></lo>
      {/each}
    </ul>
  </div>
</section>
<section>
  <h5 class="center">
    <strong>Languages <i class="bi bi-globe-americas" /></strong>
  </h5>
  <div class="container center">
    <ul>
      {#each datacv.languages as i}
        <lo><bold><i>{i}</i></bold></lo>
      {/each}
    </ul>
  </div>
</section>
<section>
  <h5 class="center">
    <strong>Expirience <i class="bi bi-person-workspace" /></strong>
  </h5>
  <div class="container-fluid">
    <div class="row row-cols-1 row-cols-md-2 ">
      {#each datacv.expirience as i}
        <div class="col">
          <article>
            <header>{i.title}</header>
            <ul>
              {#each i.desc as o}
                <li>{@html o}</li>
              {/each}
            </ul>
            <abbr>{i.lapse}</abbr>
          </article>
        </div>
      {/each}
    </div>
  </div>
</section>

<section>
  <h5 class="center">
    <strong>Education <i class="bi bi-mortarboard"></i></strong>
  </h5>
  <div class="container-fluid">
    <div class="row row-cols-1 row-cols-md-2 ">
      {#each datacv.education as i}
        <div class="col">
          <article>
            <header>{i.title} | {i.inst}</header>
            
            <abbr>{i.lapse}</abbr>
          </article>
        </div>
      {/each}
    </div>
  </div>
</section> -->
<section>
  <div>
    <h5 class="center">
      <strong>Portfolio <i class="bi bi-briefcase-fill" /></strong>
    </h5>
  </div>
  <div class="container-fluid">
    <div class="row row-cols-1 row-cols-md-2">
      {#each datacv.portfolio as i}
        <div class="col">
          <article>
            <header>
              <img src={i.logo?.src} alt="" width="60" />
              <strong>{i.name}</strong>
              
            </header>
            <abbr>{i.desc}</abbr><hr>
            <abbr>
              <ul>
                {#each i.tools as t}
                <li>{t}</li>
                {/each}
              </ul>
            </abbr>
              <small>
                {#each i.repo as r}
                  <a href={r} class="secondary" role="button" target="_blank" data-tooltip="code"><i class="bi-file-earmark-code"></i></a>
                {/each}
                {#each i.prod as p }
                <a href={p} class="contrast" role="button" target="_blank" data-tooltip="preview"><i class="bi bi-eye"></i></a>
                {/each}
              </small>
          </article>
        </div>
      {/each}
    </div>
  </div>
</section>

<footer class="back">
  <div class="container center">
    <ul>
      {#if datacv.links.github.length > 0}
        <lo
          ><a
            href={datacv.links.github}
            class=" fs-2"
            role="link"
            target="_blank"
            data-tooltip="github"><i class="bi bi-github" /></a
          ></lo
        >
      {/if}
      {#if datacv.links.linkedin.length > 0}
        <lo
          ><a
            href={datacv.links.linkedin}
            class=" fs-2"
            role="link"
            target="_blank"
            data-tooltip="linkedin"><i class="bi bi-linkedin" /></a
          ></lo
        >
      {/if}
      {#if datacv.links.twitter.length > 0}
        <lo
          ><a
            href={datacv.links.twitter}
            class=" fs-2"
            role="link"
            target="_blank"
            data-tooltip="twitter"><i class="bi bi-twitter" /></a
          ></lo
        >
      {/if}
      {#if datacv.links.portfolio.length > 0}
        <lo
          ><a
            href={datacv.links.portfolio}
            class=" fs-2"
            role="link"
            target="_blank"
            data-tooltip="portfolio"
            ><i class="bi bi-file-earmark-person-fill" /></a
          ></lo
        >
      {/if}
    </ul>
  </div>
</footer>

<style>
  .switcher {
    bottom: var(--spacing);
    width: auto;
    margin-bottom: 0;
    padding: 0.75rem;
    border-radius: 2rem;
    box-shadow: var(--card-box-shadow);
    line-height: 0.5;
    text-align: right;
  }

  .back {
    /* background-image: linear-gradient(rgba(0, 0, 255, 0), rgba(255, 255, 0, 0.021)), url("https://images.pexels.com/photos/2246476/pexels-photo-2246476.jpeg"); */
    background-color: rgb(47, 10, 78);
    padding-top: 1em;
    padding-bottom: 3px;
  }

  .center {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .fs-2 {
    font-size: calc(1.325rem + 0.9vw) !important;
    padding: 0.25em;
  }
  lo {
    margin-right: 2em;
  }
  footer {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
  }
</style>
