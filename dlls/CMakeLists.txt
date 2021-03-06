
set(SRC_HL_DLL
    aflock.cpp
    agrunt.cpp
    airtank.cpp
    animating.cpp
    animation.cpp
    apache.cpp
    barnacle.cpp
    barney.cpp
    bigmomma.cpp
    bloater.cpp
    bmodels.cpp
    bullsquid.cpp
    buttons.cpp
    cbase.cpp
    client.cpp
    combat.cpp
    controller.cpp
    crossbow.cpp
    crowbar.cpp
    defaultai.cpp
    doors.cpp
    effects.cpp
    egon.cpp
    explode.cpp
    flyingmonster.cpp
    func_break.cpp
    func_tank.cpp
    game.cpp
    gamerules.cpp
    gargantua.cpp
    gauss.cpp
    genericmonster.cpp
    ggrenade.cpp
    globals.cpp
    gman.cpp
    handgrenade.cpp
    hassassin.cpp
    headcrab.cpp
    healthkit.cpp
    hgrunt.cpp
    hornet.cpp
    hornetgun.cpp
    houndeye.cpp
    h_ai.cpp
    h_battery.cpp
    h_cine.cpp
    h_cycler.cpp
    h_export.cpp
    ichthyosaur.cpp
    islave.cpp
    items.cpp
    leech.cpp
    lights.cpp
    maprules.cpp
    monstermaker.cpp
    monsters.cpp
    monsterstate.cpp
    mortar.cpp
    mp5.cpp
    multiplay_gamerules.cpp
    nihilanth.cpp
    nodes.cpp
    observer.cpp
    osprey.cpp
    pathcorner.cpp
    plane.cpp
    plats.cpp
    player.cpp
    python.cpp
    rat.cpp
    roach.cpp
    rpg.cpp
    satchel.cpp
    schedule.cpp
    scientist.cpp
    scripted.cpp
    shotgun.cpp
    singleplay_gamerules.cpp
    skill.cpp
    sound.cpp
    soundent.cpp
    spectator.cpp
    squadmonster.cpp
    squeakgrenade.cpp
    subs.cpp
    talkmonster.cpp
    teamplay_gamerules.cpp
    tempmonster.cpp
    tentacle.cpp
    triggers.cpp
    tripmine.cpp
    turret.cpp
    util.cpp
    weapons.cpp
    world.cpp
    wpn_shared/hl_wpn_glock.cpp
    xen.cpp
    zombie.cpp
    ../game_shared/voice_gamemgr.cpp
    ../pm_shared/pm_debug.c
    ../pm_shared/pm_math.c
    ../pm_shared/pm_shared.c
)

set(HDR_HL_DLL
    activity.h
    activitymap.h
    animation.h
    basemonster.h
    cbase.h
    cdll_dll.h
    client.h
    decals.h
    defaultai.h
    doors.h
    effects.h
    enginecallback.h
    explode.h
    extdll.h
    flyingmonster.h
    func_break.h
    gamerules.h
    hornet.h
    items.h
    monsterevent.h
    monsters.h
    nodes.h
    plane.h
    player.h
    saverestore.h
    schedule.h
    scripted.h
    scriptevent.h
    skill.h
    soundent.h
    spectator.h
    squadmonster.h
    talkmonster.h
    teamplay_gamerules.h
    trains.h
    util.h
    ../common/vector.h
    weapons.h
    ../engine/eiface.h
    ../pm_shared/pm_debug.h
    ../pm_shared/pm_defs.h
    ../pm_shared/pm_info.h
    ../pm_shared/pm_materials.h
    ../pm_shared/pm_movevars.h
    ../pm_shared/pm_shared.h
)

add_library(game SHARED ${SRC_HL_DLL} ${HDR_HL_DLL})

include_directories(../dlls ../cl_dll ../public ../common ../pm_shared ../engine ../utils/vgui/include ../game_shared ../external)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /DQUIVER /DVOXEL /DQUAKE2 /DVALVE_DLL /DCLIENT_WEAPONS")

SET_TARGET_PROPERTIES(game PROPERTIES LINK_FLAGS "/DEF:\"${CMAKE_SOURCE_DIR}/dlls/hl.def\" /NODEFAULTLIB:mfc110d")

if(DEFINED MOD_FOLDER)
    if(NOT DEFINED MOD_DLL_INSTALL_FOLDER)
        set(MOD_DLL_INSTALL_FOLDER "${MOD_FOLDER}\\dlls")
    endif(NOT DEFINED MOD_DLL_INSTALL_FOLDER)

	message(STATUS "Will copy game to ${MOD_DLL_INSTALL_FOLDER}")
    add_custom_target(Copy_HL_DLL_To_Mod_Directory ALL
		COMMAND ${CMAKE_COMMAND} -E copy "${CMAKE_BINARY_DIR}\\dlls\\game.dll" ${MOD_DLL_INSTALL_FOLDER}
		COMMAND ${CMAKE_COMMAND} -E copy "${CMAKE_BINARY_DIR}\\dlls\\game.pdb" ${MOD_DLL_INSTALL_FOLDER}
    )
	add_dependencies(Copy_HL_DLL_To_Mod_Directory game)
endif(DEFINED MOD_FOLDER)
