
set(SRC_HL_CDLL
    ammo.cpp
    ammohistory.cpp
    ammo_secondary.cpp
    battery.cpp
    cdll_int.cpp
    com_weapons.cpp
    death.cpp
    demo.cpp
    entity.cpp
    events.cpp
    ev_common.cpp
    ev_hldm.cpp
    flashlight.cpp
    GameStudioModelRenderer.cpp
    geiger.cpp
    health.cpp
    hl/hl_baseentity.cpp
    hl/hl_events.cpp
    hl/hl_objects.cpp
    hl/hl_weapons.cpp
    hud.cpp
    hud_bench.cpp
    hud_benchtrace.cpp
    hud_msg.cpp
    hud_redraw.cpp
    hud_servers.cpp
    hud_spectator.cpp
    hud_update.cpp
    input.cpp
    inputw32.cpp
    interpolation.cpp
    in_camera.cpp
    menu.cpp
    message.cpp
    saytext.cpp
    statusbar.cpp
    status_icons.cpp
    StudioModelRenderer.cpp
    studio_util.cpp
    text_message.cpp
    train.cpp
    tri.cpp
    util.cpp
    vgui_ClassMenu.cpp
    vgui_ControlConfigPanel.cpp
    vgui_CustomObjects.cpp
    vgui_int.cpp
    vgui_MOTDWindow.cpp
    vgui_SchemeManager.cpp
    vgui_ScorePanel.cpp
    vgui_ServerBrowser.cpp
    vgui_SpectatorPanel.cpp
    vgui_TeamFortressViewport.cpp
    vgui_teammenu.cpp
    view.cpp
    voice_status.cpp
    ../common/parsemsg.cpp
    ../dlls/crossbow.cpp
    ../dlls/crowbar.cpp
    ../dlls/egon.cpp
    ../dlls/gauss.cpp
    ../dlls/handgrenade.cpp
    ../dlls/hornetgun.cpp
    ../dlls/mp5.cpp
    ../dlls/python.cpp
    ../dlls/rpg.cpp
    ../dlls/satchel.cpp
    ../dlls/shotgun.cpp
    ../dlls/squeakgrenade.cpp
    ../dlls/tripmine.cpp
    ../dlls/wpn_shared/hl_wpn_glock.cpp
    ../game_shared/vgui_checkbutton2.cpp
    ../game_shared/vgui_grid.cpp
    ../game_shared/vgui_helpers.cpp
    ../game_shared/vgui_listbox.cpp
    ../game_shared/vgui_loadtga.cpp
    ../game_shared/vgui_scrollbar2.cpp
    ../game_shared/vgui_slider2.cpp
    ../game_shared/voice_banmgr.cpp
    ../pm_shared/pm_debug.c
    ../pm_shared/pm_math.c
    ../pm_shared/pm_shared.c
    ../public/interface.cpp
)

set(HDR_HL_CDLL
    ammo.h
    ammohistory.h
    camera.h
    cl_dll.h
    cl_util.h
    com_weapons.h
    demo.h
    eventscripts.h
    ev_hldm.h
    GameStudioModelRenderer.h
    health.h
    hud.h
    hud_servers.h
    hud_servers_priv.h
    hud_spectator.h
    interpolation.h
    in_defs.h
    kbutton.h
    StudioModelRenderer.h
    tri.h
    util_vector.h
    vgui_ControlConfigPanel.h
    vgui_int.h
    vgui_SchemeManager.h
    vgui_ScorePanel.h
    vgui_ServerBrowser.h
    vgui_SpectatorPanel.h
    view.h
    wrect.h
    ../common/parsemsg.h
    ../game_shared/vgui_scrollbar2.h
    ../game_shared/vgui_slider2.h
    ../game_shared/voice_banmgr.h
    ../game_shared/voice_status.h
    ../pm_shared/pm_debug.h
    ../pm_shared/pm_defs.h
    ../pm_shared/pm_info.h
    ../pm_shared/pm_materials.h
    ../pm_shared/pm_movevars.h
    ../pm_shared/pm_shared.h
)

include_directories(../dlls ../cl_dll ../public ../common ../pm_shared ../engine ../utils/vgui/include ../game_shared ../external)

add_library(rjr_client SHARED ${SRC_HL_CDLL} ${HDR_HL_CDLL})

add_definitions(-DWIN32 -D_DEBUG -D_WINDOWS -DCLIENT_DLL -DCLIENT_WEAPONS -DHL_DLL)

find_file(SDL2_LIBRARY SDL2.lib ../lib/public)
find_file(VGUI_LIBRARY vgui.lib ../utils/vgui/lib/win32_vc6)
target_link_libraries(rjr_client ${SDL2_LIBRARY} ${VGUI_LIBRARY} wsock32)

Set(ALL_TARGETS ${ALL_TARGETS} "rjr_client" PARENT_SCOPE)
