== Simple Snow Hack ==

Made by JakeV

# HOW TO USE
To use the snow hack, simply replace your Caret.bmp with the one provided in this folder.
Next, apply the patches in patch.txt in Boosters Lab.
Modify Npc77's npc.tbl to use Caret.pbm as the tileset, and also check off Ignore Solid.

The first patch makes NPC 77 the snow npc.
The second patch changes the water droplet generator to spawn snow.

# CONFIGURATION
Use this XML AFTER you apply the patch
The snowhack_modify.xml will allow you to change:
 - Water droplet generator range
 - Water droplet generator chance to spawn snow
 - Snow initial X velocity
 - Snow initial Y velocity
 - Snow lifetime
 - Snow framerect

 
 
 # CSE2 Version
 ## Heres the CSE2 version that has collision with tiles, as well as collision with player
 // Yamashita (SNOW)
void ActNpc077(NPCHAR *npc) {
    RECT rect[3] = {
            {0, 240, 0+3, 240+3},
            {3, 240, 3+3, 240+3},
            {6, 240, 6+3, 240+3},
    };


    if (npc->act_wait == 0) {
        int r = Random(0,2);
        if(Random(0,3) != 0) r = 2;
        npc->rect = rect[r];
        npc->xm = Random(-0x10, 0x100);
        npc->ym = Random(0x100, 0x200);
        npc->ani_no = Random(0, 2);
        npc->surf = SURFACE_ID_CARET;
        npc->view.top = -0x200 * 5;
        npc->view.front = 0x200;
        npc->view.back = 0x200;
        npc->view.bottom = 1;
    }
    int dx = npc->x / 0x100 - gMC.x / 0x100;
    int dy = npc->y / 0x100 - gMC.y / 0x100;
    int p_dist = dx * dx + dy * dy;
    int rad = (0x200 / 0x100) * 10;
    rad *= rad;
    if (p_dist < rad) {
        npc->xm = gMC.xm / 4 + Random(-0x60, 0x60);
    }


    npc->x += npc->xm;
    npc->y += npc->ym;
    ++npc->act_wait;
    if (npc->flag & 1 || npc->flag & 4 || npc->flag & 8 || npc->flag & 0x100) {
        npc->cond = 0;
    }
    if (npc->y > gMap.length * 0x200 * 0x10){
        npc->cond = 0;
    }
}