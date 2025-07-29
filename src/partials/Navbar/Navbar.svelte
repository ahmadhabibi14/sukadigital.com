<script lang="ts">
	import { Icon } from 'svelte-icons-pack';
	import { BsList } from 'svelte-icons-pack/bs';

  let isShowMenu: boolean = $state(false);
  let pathName: string = window.location.pathname;

  const PathHome: string = '/';
  const PathAbout: string = '/about';
  const PathServices: string = '/services';
  const PathContact: string = '/contact';

  const NavbarMenus: {
    name: string;
    link: string;
  }[] = [
    { name: 'Home', link: PathHome },
    { name: 'About', link: PathAbout },
    { name: 'Services', link: PathServices }
  ];
</script>

<button
  aria-label="backdrop toggle menu"
  onclick={() => isShowMenu = !isShowMenu}
  class="{isShowMenu ? 'block' : 'hidden'} z-40 inset-0 bg-slate-700/20 h-screen fixed">
</button>

<div class="px-5 md:px-0 w-full md:w-7/12 flex flex-row items-center justify-between mx-auto">
  <div class="flex flex-row gap-3 items-center">
    <div class="flex md:hidden">
      <button
        type="button"
        onclick={() => isShowMenu = !isShowMenu}
        class="">
        <Icon
          src={BsList}
          size="30"
        />
      </button>
    </div>
    <a href="/" class="w-fit h-fit">
      <img
        src="/icons/logo.png"
        alt="Suka Digital"
        class="w-auto h-11"
      />
    </a>
  </div>
  <nav class="hidden md:flex flex-row gap-5 items-center justify-center w-fit font-semibold text-sm">
    {#each NavbarMenus as nav}
      <a
        href={nav.link}
        class="w-fit h-fit hover:text-slate-900 cursor-pointer flex flex-col gap-1 justify-center items-center
        {pathName === nav.link ? 'text-slate-800' : ''}"
      >
        <span>{nav.name}</span>
        <span class="w-[60px] h-[2px] {pathName === nav.link ? 'bg-slate-800' : 'bg-transparent'}"></span>
      </a>
    {/each}
  </nav>
  <a
    href={PathContact}
    class="md:block hidden w-fit h-fit cursor-pointer py-1 px-4 rounded-full
    bg-transparent border border-slate-800 text-sm font-semibold"
  >
    Contact
  </a>
</div>

<button
  aria-label="backdrop toggle menu"
  onclick={() => isShowMenu = !isShowMenu}
  class="{isShowMenu ? 'block' : 'hidden'} z-40 inset-0 bg-slate-700/50 h-screen fixed">
</button>

<aside
  class="{isShowMenu ? 'left-0' : '-left-[250px]'} duration-150 py-6 px-6 h-[100dvh] w-[250px] bg-white rounded-r-xl
  fixed z-50 top-0 bottom-0 flex flex-col gap-5">
  {#each NavbarMenus as nav}
    <a
      class="hover:text-slate-900 {pathName === nav.link ? 'font-semibold border border-slate-800' : ''} px-4 py-1 rounded-full w-fit"
      href={nav.link}
      onclick={()=> isShowMenu = false}
    >
      {nav.name}
    </a>
  {/each}
  <a
    class="hover:text-slate-900 {pathName === PathContact ? 'font-semibold border border-slate-800' : ''} px-4 py-1 rounded-full w-fit"
    href={PathContact}
    onclick={()=> isShowMenu = false}
  >
    Contact
  </a>
</aside>