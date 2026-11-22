# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-22T09:10:01.677912+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×36 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×128 (24h)
- 🔴 PSI_DRIFT_DETECTED×36 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×3  [2026-11-22T09:03:05]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×3  [2026-11-22T09:03:05]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-22T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=40<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-22T06:00:15]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=25 hit%=20.0% ROI=0.83 (コスト 5,400/回収 4,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-11-22T06:00:15]
- key: `ROI_STAT|S00: n=83 hit%=25.3% hit_CI[Bonf]=[14.2,40.9]% ROI=0.68 ROI_boot95=[0.41,1.00]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-22T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S00: n=83<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-22T06:00:15]
- key: `ROI_STAT|S01_NAKAANA1: n=97 hit%=30.9% hit_CI[Bonf]=[19.3,45.5]% ROI=0.79 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-22T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=97<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-22T06:00:15]
- key: `ROI_STAT|S02_TETSUBAN: n=40 hit%=42.5% hit_CI[Bonf]=[23.2,64.4]% ROI=1.18 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-11-22T06:00:15]
- key: `ORPHAN_SCAN|251 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-22T06:00:15]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=41 hit%=43.9% ROI=1.09 (コスト 9,400/回収 10,290)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-22T06:00:15]
- key: `CALIBRATION_LIVE|bt=win: n=220 pred=0.4767 actual=0.3091 error=+0.1676 (+35%) brier=0.2334 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-22T06:00:15]
- key: `CALIBRATION_LIVE|S00(win): n=83 pred=0.4349 hit=0.2530 cal_err=+0.1819 brier=0.2139 BSS=-0.13 ROI`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-22T06:00:15]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=97 pred=0.4824 hit=0.3093 cal_err=+0.1731 brier=0.2367 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-22T06:00:15]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=40 pred=0.5496 hit=0.4250 cal_err=+0.1246 brier=0.2661 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-22T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=24 pred=0.3195 actual=0.1667 gap=+0.1528`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-22T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=65 pred=0.4459 actual=0.3231 gap=+0.1228`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-22T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.50+: n=122 pred=0.5464 actual=0.3525 gap=+0.1940`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-11-22T06:00:08]
- key: `PAYOUT_RATIO_WEIRD|pid=3323 bet=300 odds=7.1 payout=630 ratio=0.30`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-11-22T06:00:08]
- key: `PAYOUT_RATIO_WEIRD|pid=3330 bet=300 odds=6.7 payout=300 ratio=0.15`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 18.42MB / last modified 2026-11-22T09:09:17.212325+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
=10), retry in 3s
2026-11-22 09:07:56,927 [INFO] scraper: odds3t: 120/120 parsed
2026-11-22 09:08:06,043 [INFO] scraper: odds3f: 20/20 parsed
2026-11-22 09:08:17,068 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=2&jcd=21&hd=20261122: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-22 09:08:28,127 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=2&jcd=21&hd=20261122: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-11-22 09:08:40,267 [INFO] scraper: odds2t: 30/30 parsed
2026-11-22 09:08:40,268 [INFO] scraper: odds2f: 15/15 parsed
2026-11-22 09:08:51,326 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=2&jcd=21&hd=20261122: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-22 09:09:02,389 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=2&jcd=21&hd=20261122: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-11-22 09:09:14,539 [INFO] scraper: odds_win: 5/6 parsed
2026-11-22 09:09:14,539 [INFO] scraper: fetch_race 21/2: boats=6 odds=190/191
2026-11-22 09:09:14,543 [INFO] predictor: CALIBRATION_MODE=on
2026-11-22 09:09:14,543 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-11-22 09:09:14,547 [INFO] run_cycle: fetched 21/2 [final]: 155 combos
2026-11-22 09:09:16,098 [INFO] race_id: notif: nid=2026112221020909 sid=S02_TETSUBAN phase=final rank=B
2026-11-22 09:09:16,472 [INFO] notifier: Discord notify OK (status=204)
2026-11-22 09:09:17,055 [INFO] notifier: Discord notify OK (status=204)
2026-11-22 09:09:17,650 [INFO] run_cycle: FINAL S02_TETSUBAN 芦屋2R B
2026-11-22 09:09:47,175 [INFO] scraper: odds3t: 120/120 parsed
2026-11-22 09:09:56,308 [INFO] scraper: odds3f: 20/20 parsed

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 52
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 52
  }
]
```

## Phase別通知記録 (24h)
{'final': 19, 'result': 7, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 207
  FINAL_MISSING: 128
  PSI_DRIFT_DETECTED: 36
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 5
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 8 | 3 | 2,400 | 1,860 | -540 | 0.775 |
| S01_NAKAANA1 | 17 | 6 | 3,400 | 2,920 | -480 | 0.859 |
| S02_TETSUBAN | 6 | 3 | 1,200 | 2,200 | +1,000 | 1.833 |

## 直近アラート (24h・新しい順)
```
[09:03:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:03:04] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 190, "n_recent": 30, "psi": 0.486}
[08:02:52] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:02:52] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 190, "n_recent": 30, "psi": 0.486}
[06:00:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:04] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 190, "n_recent": 30, "psi": 0.486}
[23:58:04] FINAL_MISSING: {"deadline": "2026-11-21T14:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112105091416", "sid": "S01_NAKAANA1"}
[23:56:04] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 190, "n_recent": 30, "psi": 0.486}
[23:54:04] FINAL_MISSING: {"deadline": "2026-11-21T13:11:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112121101311", "sid": "S00"}
[23:48:04] FINAL_MISSING: {"deadline": "2026-11-21T10:57:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112113021057", "sid": "S00"}
```

## 本日残レース: 163件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 5件 締切済
- 通知発射: scan=1 nid / final=1 nid / result=0 nid
- predictions: 1 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 212R | win | 1 | 0.5735 | 2.2 | 1.26 | 200 | scan=2.2 drift=+0.0% | 09:09:14 |
| S00 | 136R | win | 1 | 0.5891 | 4.8 | 2.83 | 300 | scan=- drift=- | 12:57:00 |
| S01_NAKAANA1 | 225R | win | 1 | 0.5735 | 4.3 | 2.47 | 200 | scan=- drift=- | 12:44:23 |
| S01_NAKAANA1 | 045R | win | 1 | 0.3177 | 4.6 | 1.46 | 200 | scan=- drift=- | 12:38:22 |
| S02_TETSUBAN | 135R | win | 1 | 0.5174 | 2.7 | 1.40 | 200 | scan=2.7 drift=+0.0% | 12:29:13 |
| S01_NAKAANA1 | 023R | win | 1 | 0.4111 | 4.3 | 1.77 | 200 | scan=4.1 drift=+4.9% | 11:37:25 |
| S00 | 042R | win | 1 | 0.4989 | 5.4 | 2.69 | 300 | scan=- drift=- | 11:17:13 |
| S01_NAKAANA1 | 052R | win | 1 | 0.5891 | 3.1 | 1.83 | 200 | scan=- drift=- | 10:59:24 |
| S01_NAKAANA1 | 1410R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=4.8 drift=-25.0% | 12:53:02 |
| S01_NAKAANA1 | 218R | win | 1 | 0.5123 | 3.1 | 1.59 | 200 | scan=- drift=- | 12:08:26 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 16 | +0.3% | -26.8% | +55.6% | 6 | 0 | 8 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 330.7s |
| **Latency** (scan→final max) | 695.1s |
| **Traffic** (notifications 24h) | 52 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 220 | 0.4767 | 0.3091 | +0.1676 | 🟡+35% | 0.2334 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 83 | 0.4349 | 0.2530 | 0.2139 | 🔴-0.13 | 0.68 |
| S01_NAKAANA1 | win | 97 | 0.4824 | 0.3093 | 0.2367 | 🔴-0.11 | 0.792 |
| S02_TETSUBAN | win | 40 | 0.5496 | 0.4250 | 0.2661 | 🔴-0.09 | 1.183 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 89 | 0.4118 | 0.2809 | 🔴+0.1309 |
| 0.50+ | 122 | 0.5464 | 0.3525 | 🔴+0.1940 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 208 | 0.818 |
| win | <5.0 | ✅learned | 378 | 0.737 |
| win | <10.0 | ✅learned | 160 | 0.449 |
| win | <20.0 | ✅learned | 48 | 0.252 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-11-22T09:10:01.677912+09:00_