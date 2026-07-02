# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-02T13:20:02.334107+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×23 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×40 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×23 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×17  [2026-07-02T13:03:06]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×17  [2026-07-02T13:03:06]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×17  [2026-07-02T13:03:06]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×20  [2026-07-02T13:00:33]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-07-02T13:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×26  [2026-07-02T11:50:51]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×18  [2026-07-02T10:35:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-02T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=72<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-07-02T06:00:13]
- key: `ORPHAN_SCAN|152 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-02T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=164<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-02T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1819 actual=0.3333 gap=-0.1514`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-02T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=12 pred=0.2253 actual=0.0833 gap=+0.1420`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-02T06:00:13]
- key: `DRIFT_BUCKET|drift ≤-30%: n=37 hit%=27.0% ROI=0.83 (コスト 10,800/回収 8,940)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-07-02T06:00:13]
- key: `ROI_STAT|S00: n=164 hit%=26.2% hit_CI[Bonf]=[17.6,37.1]% ROI=0.70 ROI_boot95=[0.51,0.92]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-02T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=140 hit%=30.7% hit_CI[Bonf]=[20.8,42.8]% ROI=0.81 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-02T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=140<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-02T06:00:13]
- key: `ROI_STAT|S02_TETSUBAN: n=72 hit%=29.2% hit_CI[Bonf]=[16.5,46.1]% ROI=0.45 ROI_boot95=[0.2`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-02T06:00:13]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=40 hit%=22.5% ROI=0.57 (コスト 9,500/回収 5,400)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-02T06:00:13]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=83 hit%=30.1% ROI=0.76 (コスト 19,400/回収 14,680)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-02T06:00:13]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=26 hit%=30.8% ROI=1.03 (コスト 6,300/回収 6,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.59MB / last modified 2026-07-02T13:19:35.538544+09:00

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
:19,072 [INFO] scraper: odds2f: 15/15 parsed
2026-07-02 13:19:20,182 [INFO] scraper: odds_win: 5/6 parsed
2026-07-02 13:19:20,182 [INFO] scraper: fetch_race 16/6: boats=6 odds=190/191
2026-07-02 13:19:20,194 [INFO] predictor: CALIBRATION_MODE=on
2026-07-02 13:19:20,194 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-07-02 13:19:20,203 [INFO] run_cycle: fetched 16/6 [final]: 155 combos
2026-07-02 13:19:20,427 [INFO] race_id: notif: nid=2026070216061322 sid=S01_NAKAANA1 phase=final rank=
2026-07-02 13:19:20,788 [INFO] notifier: Discord notify OK (status=204)
2026-07-02 13:19:21,156 [INFO] notifier: Discord notify OK (status=204)
2026-07-02 13:19:21,161 [INFO] run_cycle: RETREAT S01_NAKAANA1 児島6R
2026-07-02 13:19:24,674 [INFO] scraper: odds3t: 120/120 parsed
2026-07-02 13:19:25,764 [INFO] scraper: odds3f: 20/20 parsed
2026-07-02 13:19:27,045 [INFO] scraper: odds2t: 30/30 parsed
2026-07-02 13:19:27,046 [INFO] scraper: odds2f: 12/15 parsed
2026-07-02 13:19:28,256 [INFO] scraper: odds_win: 5/6 parsed
2026-07-02 13:19:28,256 [INFO] scraper: fetch_race 04/4: boats=6 odds=187/191
2026-07-02 13:19:28,265 [INFO] predictor: CALIBRATION_MODE=on
2026-07-02 13:19:28,267 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-07-02 13:19:28,273 [INFO] run_cycle: fetched 04/4 [scan]: 155 combos
2026-07-02 13:19:31,834 [INFO] scraper: odds3t: 120/120 parsed
2026-07-02 13:19:32,949 [INFO] scraper: odds3f: 20/20 parsed
2026-07-02 13:19:34,082 [INFO] scraper: odds2t: 30/30 parsed
2026-07-02 13:19:34,083 [INFO] scraper: odds2f: 15/15 parsed
2026-07-02 13:19:35,187 [INFO] scraper: odds_win: 4/6 parsed
2026-07-02 13:19:35,187 [INFO] scraper: fetch_race 21/11: boats=6 odds=189/191
2026-07-02 13:19:35,197 [INFO] predictor: CALIBRATION_MODE=on
2026-07-02 13:19:35,197 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-07-02 13:19:35,205 [INFO] run_cycle: fetched 21/11 [scan]: 154 combos
2026-07-02 13:19:35,347 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 20, 'result': 11, 'scan': 21}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 140
  FINAL_MISSING: 40
  CIRCUIT_BREAKER_TRIP: 23
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 4
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 39 | 11 | 11,700 | 7,920 | -3,780 | 0.677 |
| S01_NAKAANA1 | 41 | 15 | 8,200 | 7,160 | -1,040 | 0.873 |
| S02_TETSUBAN | 13 | 3 | 2,600 | 800 | -1,800 | 0.308 |

## 直近アラート (24h・新しい順)
```
[13:03:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:03:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[13:01:27] CIRCUIT_BREAKER_TRIP: {"cost": 11700, "kind": "CIRCUIT_BREAKER_TRIP", "n": 39, "payout": 7920, "roi_7d": 0.677, "sid": "S00"}
[13:00:31] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 7.6, "baseline_n_days": 7, "baseline_stdev": 2.6, "hour": 13, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 2, "z_score": -2.11}
[12:45:22] FINAL_MISSING: {"deadline": "2026-07-02T12:15:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070216041215", "sid": "S00"}
[12:43:21] FINAL_MISSING: {"deadline": "2026-07-02T11:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070216021112", "sid": "S00"}
[12:38:31] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.208, "baseline_mean": 0.808, "baseline_stdev": 0.09, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.6, "today_scan_count": 5, "z_score": -2.32}
[12:02:35] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:02:35] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[12:02:35] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.308, "baseline_mean": 0.808, "baseline_stdev": 0.09, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 4, "z_score": -3.44}
```

## 本日残レース: 105件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 51件 締切済
- 通知発射: scan=6 nid / final=6 nid / result=2 nid
- predictions: 2 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 164R | win | 1 | 0.4111 | 2.5 | 1.03 | 200 | scan=- drift=- | 12:12:21 |
| S01_NAKAANA1 | 234R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 09:59:31 |
| S02_TETSUBAN | 209R | win | 1 | 0.5123 | 2.1 | 1.08 | 200 | scan=- drift=- | 21:25:22 |
| S01_NAKAANA1 | 203R | win | 1 | 0.5891 | 4.2 | 2.47 | 200 | scan=3.5 drift=+20.0% | 18:31:21 |
| S01_NAKAANA1 | 076R | win | 1 | 0.5994 | 4.0 | 2.40 | 200 | scan=3.3 drift=+21.2% | 18:01:21 |
| S00 | 073R | win | 1 | 0.4111 | 6.2 | 2.55 | 300 | scan=7.6 drift=-18.4% | 16:34:21 |
| S02_TETSUBAN | 1610R | win | 1 | 0.5174 | 2.0 | 1.03 | 200 | scan=- drift=- | 15:32:32 |
| S00 | 028R | win | 1 | 0.5174 | 9.5 | 4.92 | 300 | scan=- drift=- | 14:13:33 |
| S01_NAKAANA1 | 1012R | win | 1 | 0.4989 | 3.6 | 1.80 | 200 | scan=3.5 drift=+2.9% | 13:57:23 |
| S00 | 087R | win | 1 | 0.4111 | 18.0 | 7.40 | 300 | scan=6.0 drift=+200.0% | 13:39:23 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 55 | +11.8% | -68.9% | +584.6% | 22 | 12 | 34 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 522.2s |
| **Latency** (scan→final max) | 616.1s |
| **Traffic** (notifications 24h) | 52 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 377 | 0.4810 | 0.2838 | +0.1972 | 🟡+41% | 0.2391 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 164 | 0.4415 | 0.2622 | 0.2224 | 🔴-0.15 | 0.704 |
| S01_NAKAANA1 | win | 140 | 0.4955 | 0.3071 | 0.2441 | 🔴-0.15 | 0.814 |
| S02_TETSUBAN | win | 73 | 0.5421 | 0.2877 | 0.2671 | 🔴-0.30 | 0.445 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1819 | 0.3333 | 🔴-0.1514 |
| 0.20-0.30 | 12 | 0.2253 | 0.0833 | 🔴+0.1420 |
| 0.30-0.50 | 128 | 0.4237 | 0.2344 | 🔴+0.1893 |
| 0.50+ | 225 | 0.5444 | 0.3244 | 🔴+0.2199 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 49 | 0.725 |
| win | <5.0 | ✅learned | 111 | 0.716 |
| win | <10.0 | ✅learned | 61 | 0.483 |
| win | <20.0 | ✅learned | 18 | 0.212 |
| win | <50.0 | ⚠️fallback | 2 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-07-02T13:20:02.334107+09:00_